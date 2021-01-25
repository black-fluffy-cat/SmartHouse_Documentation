Setup server:
1. Launch ktorsmarthouseserver
2. Setup ngrok with proper config at server side
Config file location: /home/j/.ngrok2/ngrok.yml
Sample config:

authtoken: [proper_authtoken]

tunnels:
 tcp_ssh:
  proto: tcp
  addr: 22
 http_server:
  proto: http
  addr: 5000
  bind_tls: true
 http_server_1:
  proto: http
  addr: 8080
  bind_tls: true
  
Setup raspberry:
1. Launch raspberry
2. Install flask_api as user AND as root
3. Execute this command as user AND as root for VNC to work properly
	vncserver -nolisten tcp -nevershared -Authentication VncAuth :1
	Then give password for vnc
	And next time when launching through rc.local it will not ask for password
4. Execute sudo raspi-config and enable camera interface
3. Make sure VNC script is launched while boot
4. Setup ngrok with proper config at Raspberry side
5. Make sure ngrok is launched while boot
6. Make sure server script is launched while boot
7. For steps 2,3,4 sample rc.local file is included in directory with this readme
8. Check raspberry ngrok address
9. Make Postman call to raspberry to set proper server url
10. Raspberry should be sending heartbeat calls and respond to alertPhoto calls from now
11. Setup ngrok with proper config at Raspberry side
12. https://raspberrypi.stackexchange.com/questions/11631/how-to-setup-multiple-wifi-networks

Script launch while boot:
1. Create script: 
2. Add script to /etc/init.d
3. Make script executable by adding +x permissions to it
4. Execute command: "sudo update-rc.d [script_name] defaults" for 'install System-V style init script links'
- check this https://howchoo.com/g/mwnlytk3zmm/how-to-add-a-power-button-to-your-raspberry-pi
5. From experience doing steps 1-4 does not make scripts to launch after boot.
6. Instead add this line to /etc/rc.local - sh [path_to_script]
7. Double check if added lines works by simply executing rc.local script

Setup Ngrok at Raspberry:
1. https://www.techcoil.com/blog/how-to-put-your-raspberry-pi-server-on-the-internet-with-ngrok/

Setup Raspberry Pi 4 with Pi Ubuntu 20.04:
1. Problems with vnc - errors with fonts - UNRESOLVED
2. Make /etc/rc.local executable - is not by default
3. Execute rc.local commands as user, '$ su - user -c "cmd" &'
4. Then logs files saves into proper directory

Notes:
1. Server saves NgrokAddresses logs to file - FIXED
2. Server saves Monitoring logs to file - FIXED
3. Raspberry saves last known server address to file, if raspberry will reset it will use last known address, uses default if file not exists
