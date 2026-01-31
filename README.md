# Windows Server Host Setup
1. On your usual client machine (different from your intended server machine), navigate to `C:\Program Files\Oculus\Software\Software\ready-at-dawn-echo-arena\_local\config.json` (for PC) OR `/sdcard/readyatdawn/config.json` (for Quest). Replace the contents of the config file with the following, and update it with your own information:
```
{
    "apiservice_host":  "http://g.echovrce.com:80/api",
    "configservice_host":  "ws://g.echovrce.com:80/config",
    "loginservice_host":  "ws://g.echovrce.com:80/login?discordid=YOURDISCORDID&password=YOURPASSWORD",
    "matchingservice_host":  "ws://g.echovrce.com:80/matching",
    "serverdb_host":  "ws://g.echovrce.com:80/serverdb?discordid=YOURDISCORDID&password=YOURPASSWORD",
    "transactionservice_host":  "ws://g.echovrce.com:80/transaction",
    "publisher_lock":  "echovrce"
}
```

> [!WARNING]
> The password used in your config file should not be any password you typically use.

2. Set your server machine's connection to a private network in Settings > Network & Internet > Properties > Private Network
3. Give your server machine has a static IP on your local network. (e.g., 192.168.1.100, 10.0.0.100, etc.)

> [!TIP]
> Check if your IP address is behind a CGNAT. (See google/chatgpt for details)
>
> If you are behind a CGNAT, skip step 4, but have a domain/tunnel service ready to connect. (playit.gg, cloudflare, etc.)

4. Forward port 6792 TCP/UDP to your server machine. For each additional gameserver you want to run, increase the max value by 1. (e.g., for 3 servers, forward 6792-6794)
5. Install Echo on your server machine via [Mia's Installer](https://github.com/BL00DY-C0D3/Echo-VR-Installer/releases). Download and extract the [updated hosting files](https://github.com/user-attachments/files/24868223/newhostfiles.zip) onto your server machine.
6. Copy the new `config.json` file you used to log in on your regular client machine to the PC config location on your server machine.

> [!NOTE]
> If you were given a specific region ID to use, add `&regions=REGIONID` after your password on the `serverdb_host` line of the config file. Otherwise, you can leave it out.
> 
> If you are hosting behind a domain or tunnel service (cloudflare, noip, playit, etc.), add `&serveraddr=IP:PORT` to the end of the `serverdb_host` line. Replace the `IP` and `PORT` values with the external IP and port of your domain/tunnel.

7. Extract the contents of `gunpatch.zip` to `\...\ready_at_dawn_echo_arena\` and run `patch.bat`.
8. Put `dbgcore.dll` and `pnsradgameserver.dll` in the `\...\ready_at_dawn_echo_arena\bin\win10\` directory. Replace any duplicate files.
9. Download the server monitor to auto-restart in the event of a crash [here](https://github.com/EchoTools/Echo-VR-Server-Error-Monitoring-Windows/tree/main).
10. __If you are running more than 3 servers__, go to `...\ready-at-dawn-echo-arena\sourcedb\rad15\json\r14\config\netconfig_dedicatedserver.json` and update `retries` to the number of servers you are running plus 1.

### Optional, but highly recommended:
- Ensure your router is not blocking P2P traffic to the server. This is especially necessary for hosts with UniFi hardware.
