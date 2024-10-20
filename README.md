Role Name
=========

An ansible role to install dockerized Counter-Strike 2 dedicated server

Requirements
------------

This role uses [joedwards32/cs2](https://hub.docker.com/r/joedwards32/cs2) docker image, hence all its requirements should be met

Role Variables
--------------

Required variables are:

```
srcds_token: # Game Server Token from https://steamcommunity.com/dev/managegameservers
cs2_rconpw: # (RCON password)
cs2_pw: # (CS2 server password)
```

Optional variables:
```
# Server configuration

restart_cs2_server: false # Restart server if exists, if not create
cs2_data_dir: /data/cs2-data # Persistent data volume mount point inside container
container_name: cs2-dedicated # Container name for cs2 server
cs2_servername: cs2-dedicated # (Set the visible name for your private server)
steamappvalidate: 1 # (0 - no validation, 1 - enable validation)
cs2_cheats: 0 # (0 - disable cheats, 1 - enable cheats)
cs2_port: 27015 # (CS2 server listen port tcp_udp)
cs2_server_hibernate: 0 # (Put server in a low CPU state when there are no players. 0 - hibernation disabled, 1 - hibernation enabled)
cs2_rcon_port: "" # (Optional, use a simple TCP proxy to have RCON listen on an alternative port. Useful for services like 
                  # AWS Fargate which do not support mixed protocol ports.)
cs2_lan: 0 # (0 - LAN mode disabled, 1 - LAN Mode enabled)
cs2_maxplayers: 20 # (Max players)
cs2_additional_args: "" # (Optional additional arguments to pass into cs2)
cs2_cfg_url: "" # HTTP/HTTPS URL to fetch a Tar Gzip bundle of configuration files/mods

# Game modes
cs2_gamealias: "" # (Game type, e.g. casual, competitive, deathmatch.) 
                  # See https://developer.valvesoftware.com/wiki/Counter-Strike_2/Dedicated_Servers)
cs2_gametype: 0 # (Used if CS2_GAMEALIAS not defined.) See https://developer.valvesoftware.com/wiki/Counter-Strike_2/Dedicated_Servers)
cs2_gamemode: 0 # (Used if CS2_GAMEALIAS not defined.) See https://developer.valvesoftware.com/wiki/Counter-Strike_2/Dedicated_Servers)
cs2_mapgroup: "mg_active" # (Map pool. Ignored if Workshop maps are defined.)
cs2_startmap: "de_inferno" # (Start map. Ignored if Workshop maps are defined.)

# Workshop Maps
cs2_host_workshop_collection: "" # The workshop collection to use
cs2_host_workshop_map: "" # The workshop map to use.

# Bots
cs2_bot_difficulty: 1  # (0 - easy, 1 - normal, 2 - hard, 3 - expert)
cs2_bot_quota: 0 # (Number of bots)
cs2_bot_quota_mode: "" # (fill, competitive)

# TV
tv_autorecord: 0 # Automatically records all games as CSTV demos: 0=off, 1=on.
tv_enable: 0 # Activates CSTV on server: 0=off, 1=on.
tv_port: 27020 # Host SourceTV port
tv_pw: # CSTV password for clients
tv_relay_pw: # CSTV password for relay proxies
tv_maxrate: 0 # World snapshots to broadcast per second.
tv_delay: 0 # CSTV broadcast delay in seconds

# Logs
cs2_log: "on" # 'on'/'off'
cs2_log_money: 0 # Turns money logging on/off: 0=off, 1=on
cs2_log_detail: 0 # Combat damage logging: (0=disabled, 1=enemy, 2=friendly, 3=all)
cs2_log_items: 0 # Turns item logging on/off: (0=off, 1=on)
```

required_vars - is technical variable, used for validation of other variables

Dependencies
------------

This role depends only on builtin ansible tools

Example Playbook
----------------

    - hosts: cs2-server
      become: true
      vars:
        srcds_token: "XXXXXXXXXXXXXXXXXXXXXXX"
        cs2_rconpw: 'XXXXXXXXXXXXXXXXXXXXXXX'
        cs2_pw: 'XXXXXXXXXXXXXXXXXXXXXXX'
      roles:
      - name: cs2-server-role

License
-------

BSD

