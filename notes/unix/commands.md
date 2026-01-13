**list processes**
- running on a port: `sudo lsof -i :<PORT>`
- all listening ports and processes: `sudo lsof -i -P -n`
- find a specific port with `grep`: `sudo lsof -i -P -n | grep ':<PORT>'`

**kill process**
`pkill `