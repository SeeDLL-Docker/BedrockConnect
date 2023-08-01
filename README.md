# BedrockConnect Docker

## Because I didn't seem to see that the developer has uploaded a Docker image, I packaged this image.

## Developer's Github: https://github.com/Pugmatt/BedrockConnect
### note: I have set this image to be automatically built every three days, so that the project's image can be updated at any time.
-------------------


![Logo](https://i.imgur.com/H9zVzGT.png)


In Minecraft Bedrock Edition, players on Xbox One, Nintendo Switch, and PS4 can only play on Mojang/Microsoft approved "featured servers". These players cannot join the server by IP/address. This is a problem for me and others as the Java Edition server community is one of the major parts of what makes Minecraft what it is, and what makes what is now considered a "Mojang Server Partner" server what it is today. I wanted to fix this, so I made a solution that anyone can easily set up.

BedrockConnect is an easy-to-use solution for Minecraft Bedrock Edition players on Xbox One, Nintendo Switch, PS4 to join any server IP, while also accessing a server list that allows you to manage your server list. It doesn't require any downloads, just a few changes to the settings.


In this example, you can directly fill in the startup command in the container startup command with related configuration parameters.

The location of the jar package: /app

Start method: 

```
java -jar BedrockConnect-1.0-SNAPSHOT.jar [selected parameters]
```


The specific usage instructions are quoted from the developer's introduction. For more detailed instructions, please refer to the developer's Github.


Run the jar with the following command
```
java -jar BedrockConnect-1.0-SNAPSHOT.jar nodb=true
```
(```nodb=true``` allows the software to run without a database. If you want to use a database, remove this argument)

The following arguments can be placed in the startup command to ajust settings:

| Argument  | Description | Default Value |
| ------------- | ------------- | ------------- |
| mysql_host  | MySQL Host  | localhost |
| mysql_db | MySQL Database Name  | bedrock-connect |
| mysql_user | MySQL Username  | root |
| mysql_pass | MySQL Password  |  |
| server_limit | How many servers a new player can have in their serverlist  | 100 |
| port | Port of the server (Should only be changed for debugging on PC. Port needs to be on 19132 for the bypass to work on game consoles) | 19132 |
| bindip | IP that the BedrockConnect server will bind to | 0.0.0.0 |
| nodb | If true, use JSON files for data instead of MySQL | false |
| generatedns | If true, generate a DNS zone file using user input (Only needed if you're using the mod0Umleitung DNS software) | false |
| kick_inactive | If true, players will be kicked after 10 minutes of inactivity with the serverlist UI | true |
| custom_servers| Sets the path to a custom server file, for specifying your servers in the list for all players. See  Developer's Github |  |
| user_servers | If true, players can add and remove servers on the serverlist. If false, the options are hidden. | true |
| featured_servers | If true, the featured servers will be displayed in the serverlist.  If false, the servers are hidden. | true |
| whitelist | Specify file containing list of whitelisted players. (Should be a text file with the player names specified on seperate lines) | |
| fetch_featured_ips | If true, dynamically grab the featured server IPs from the domain names. If false, a file ```featured_server_ips.json``` will be generated, containing the hard-coded featured server IPs, and to allow changing them if needed.  | true |
| language | Specify a file containing language customizations. See Developer's Github | |

Docker Default example:
```
docker run --name Minecraft \
    --network host \
    -p 19132:19132/udp \
    -d seedll/bedrockconnect
```

Docker MySQL example:
```
docker run --name Minecraft \
    --network host \
    -p 19132:19132/udp \
    -d seedll/bedrockconnect java -Xms256M -Xmx256M -jar BedrockConnect-1.0-SNAPSHOT.jar  \
    mysql_host=123.234.345.456 \
    mysql_db=BedrockConnect \
    mysql_user=minecraft \
    mysql_pass=minecraft \
    server_limit=200
```
