**discover processes**
- running on a port: `sudo lsof -i :<PORT>`
- all listening ports and processes: `sudo lsof -i -P -n`
- find a specific port with `grep`: `sudo lsof -i -P -n | grep ':<PORT>'`
- show which command started the process: `ps -p 12345 -o pid,ppid,user,cmd`

**kill processes**
`sudo kill <PID>`
- forceful kill (when the above is unresponsive): `kill -9 <PID>`
- verify with `ps -p <PID>` 

**long running processes**
- `nohup long-running-scrip.sh &` -> `nohup` ignores logout signals and `&` detaches from the shell, running it on background
- `<command> & disown` -> `&` runs on background and `disown` gives full independency
- for a process already running (not on background) to start running on background, simply:
  1. suspend it with `Ctrl + Z`
  2. `bg`
  3. `disown`