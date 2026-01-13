**list processes**
- running on a port: `sudo lsof -i :<PORT>`
- all listening ports and processes: `sudo lsof -i -P -n`
- find a specific port with `grep`: `sudo lsof -i -P -n | grep ':<PORT>'`
- show which command started the process: `ps -p 12345 -o pid,ppid,user,cmd`

**kill process**
`kill <PID>`
- forceful kill (when the above is unresponsive): `kill -9 <PID>`
- verify with `ps -p <PID>` -> 