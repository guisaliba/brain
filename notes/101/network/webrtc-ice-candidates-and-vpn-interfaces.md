## why discord voice can fail when tailscale is present

Discord voice in the browser uses WebRTC. WebRTC does not behave like normal page loading.

when Chromium loads `discord.com`, the request normally follows the OS routing table:

```text
discord.com -> default route -> wlan0
```

but when Discord starts voice or video, WebRTC starts ICE negotiation. ICE means Interactive Connectivity Establishment. its job is to find a usable network path for real-time UDP media.

that process does not only ask "what is the default route?". it asks a broader question:

```text
which local network paths might be usable for real-time media?
```

so Chromium enumerates local interfaces and may see things like:

```text
wlan0
tailscale0
docker0
lo
```

then WebRTC creates and tests ICE candidates from those networks.

## what an ICE candidate is

an ICE candidate is a possible address/path that WebRTC can try for media traffic.

common candidate types:

| candidate | meaning |
|---|---|
| host | local interface address, such as LAN or VPN IP |
| srflx | server-reflexive address discovered through STUN, usually public NAT mapping |
| relay | TURN relay address, used when direct paths fail |
| prflx | peer-reflexive address discovered during connectivity checks |

WebRTC gathers candidates, gives them priorities, exchanges them with the remote side, and runs connectivity checks. the final path is not picked randomly. it is chosen by the ICE algorithm based on candidate type, priority, reachability, and network checks.

## why the default interface is not enough

the OS default route means:

```text
if there is no more specific route, send normal traffic through this interface
```

on this machine, the normal default route was `wlan0`. that means regular HTTPS traffic to Discord uses Wi-Fi.

WebRTC is different because it may bind UDP sockets to specific local addresses or gather candidates from specific interfaces. a VPN/TUN interface like `tailscale0` can therefore participate in candidate gathering even when it is not the default route.

so this is wrong:

```text
default route is wlan0, therefore WebRTC can only use wlan0
```

more accurate:

```text
default route is wlan0, but WebRTC can still enumerate and consider other interfaces as candidate sources
```

## why tailscale0 can confuse Chromium/WebRTC

Tailscale creates a TUN interface called `tailscale0`.

when Tailscale is up, `tailscale0` usually has addresses like:

```text
100.x.y.z
fd7a:115c:a1e0::...
```

when Tailscale is down, the interface may still exist. on this machine it still had a link-local IPv6 address:

```text
tailscale0 fe80::...
```

Chromium can see the interface and treat it as network-relevant. because WebRTC intentionally considers multiple local paths, `tailscale0` may affect candidate gathering or candidate ranking.

there is a known class of Chromium/Linux bugs around WebRTC and VPN/TUN interfaces. the symptom can look like Discord permanently stuck on RTC connecting. this is not necessarily because Tailscale blocks Discord. it can be because Chromium gives WebRTC bad candidate information or mishandles the VPN-like interface.

the important distinction:

```text
Tailscale did not need to be opened for inbound Discord traffic.
Chromium needed to stop using the Tailscale interface as a WebRTC candidate source.
```

## why opening ports on tailscale0 is the wrong fix

opening inbound UDP on `tailscale0` is usually solving the wrong problem.

Discord browser voice wants to negotiate outbound UDP media paths to Discord's infrastructure, often using STUN/TURN. the problem here is not that remote Discord users need to enter this machine through the tailnet.

opening the interface could increase local attack surface and does not necessarily fix bad ICE candidate selection.

if the issue is Chromium selecting or exposing bad candidates, the safer fix is to constrain Chromium's WebRTC candidate gathering.

## recommended fix

configure Chromium's WebRTC IP handling policy:

```json
{
  "WebRtcIPHandlingPolicy": "default_public_interface_only"
}
```

on Arch/Chromium, a managed policy can live at:

```text
/etc/chromium/policies/managed/webrtc-ip-handling.json
```

after restarting Chromium, `chrome://policy` should show:

```text
WebRtcIPHandlingPolicy = default_public_interface_only
```

## what this policy actually changes

the policy tells Chromium:

```text
for WebRTC, only use the default public interface/address
```

with the normal default route on `wlan0`, Discord WebRTC should gather candidates from the normal internet path instead of considering `tailscale0`.

this is narrow in scope:

| thing | changed? |
|---|---|
| Tailscale daemon | no |
| Tailscale ACLs | no |
| Tailscale SSH | no |
| Cloudflare tunnel | no |
| Linux routing table | no |
| firewall rules | no |
| inbound UDP ports | no |
| Chromium WebRTC candidate gathering | yes |

normal browsing can still reach tailnet IPs if the OS routing table allows it. the policy affects WebRTC candidate exposure/selection, not all browser networking.

## why this is better than tailscale down/up

`tailscale down`, joining the Discord call, and `tailscale up` works because the bad interface is removed or made less relevant during ICE startup.

but that is only a timing workaround.

the managed Chromium policy is persistent. it keeps Tailscale up and makes WebRTC ignore non-default public interfaces for candidate gathering.

## when this policy may not be enough

if Tailscale is used as an exit node, then Tailscale may become the default route. in that case, `default_public_interface_only` may still choose Tailscale because it is the default public path.

if Chromium has a lower-level bug that still triggers despite the policy, the next safer workaround is network isolation for the browser/app, for example running Discord/Chromium in a namespace that only exposes `wlan0`.

one example from the Tailscale issue was:

```bash
firejail --net=wlan0 --noprofile ...
```

that is heavier than a browser policy because it changes the whole process network namespace. it is a fallback, not the first fix.

## mental model

normal web traffic:

```text
URL -> DNS -> TCP/TLS -> OS default route -> wlan0
```

WebRTC media setup:

```text
enumerate interfaces -> gather ICE candidates -> exchange candidates -> test UDP paths -> select working pair
```

therefore:

```text
default route affects WebRTC, but does not fully determine WebRTC behavior
```

VPN/TUN interfaces like `tailscale0` can matter even when they are not the default route.

## references

- https://github.com/tailscale/tailscale/issues/10396
- https://github.com/tailscale/tailscale/issues/10396#issuecomment-3871203280
- https://github.com/tailscale/tailscale/issues/10396#issuecomment-4416242984
- https://issues.chromium.org/issues/474435503
- [[sockets]]
- [[ips-and-ports]]
