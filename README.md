# SC4MP Server

A multiplayer gameserver for the PC videogame [SimCity 4](https://en.wikipedia.org/wiki/SimCity_4). Uses [python 3.8.10](https://www.python.org/downloads/release/python-3810/) and [py2exe](https://www.py2exe.org/). Built to work with the [SC4MP Client](https://github.com/kegsmr/sc4mp-client).


# Installation and Usage

Download the latest release and follow the instructions included in the Readme.html.


# Compiling

To compile the source code, run the setup.py script.


# API

This section is meant for developers using the server API. Here you can find examples of requests and responses from the server API, useful for creating a server scanner or client appplication for the SC4MP network.

**NOTE:** this documentation will apply to version 0.4.0 and later


## Add server
Adds the requesting server to the requested server's server list queue.

#### Request
```
add_server <port>
```

#### Response
none


## Check password
Returns "y" if the password provided is correct, otherwise "n".

#### Request
```
check_password <password>
```

#### Response
```
y
```
or
```
n
```


## Info
Returns server info in a JSON dictionary.

#### Request
```
info
```

#### Response
```
{  
    "server_id": <server_id>,  
    "server_name": <server_name>,  
    "server_description": <server_description>,  
    "server_url": <server_url>,  
    "server_version": <server_version>,  
    "private": <private>,  
    "password_enabled": <password_enabled>,  
    "user_plugins_enabled": <user_plugins_enabled>  
}
```


## Password enabled
Returns "y" if the server requires a password, otherwise "n".

#### Request
```
password_enabled
```

#### Response
```
y
```
or
```
n
```


## Ping
Returns "pong".

#### Request
```
ping
```

#### Response
```
pong
```


## Plugins
Requests plugins from the server. (TODO: implement)

#### Request
```
plugins
```
or
```
plugins <version> <user_id> <password>
```

#### Response
```
[
	[<file_1_md5>, <file_1_size>, <file_1_relpath>],
	[<file_2_md5>, <file_2_size>, <file_2_relpath>],
	...
	[<file_n_md5>, <file_n_size>, <file_n_relpath>]
]
```

#### Request
```
[
    [<file_1_md5>, <file_1_size>, <file_1_relpath>],
    [<file_2_md5>, <file_2_size>, <file_2_relpath>],
    ...
    [<file_n_md5>, <file_n_size>, <file_n_relpath>]
]
```

#### Response
```
<file_1_data>
<file_2_data>
...
<file_n_data>
```


## Private
Returns "y" if the server's plugins and regions require a request header, otherwise "n".

#### Request
```
private
```

#### Response
```
y
```
or
```
n
```


## Regions
Requests regions from the server. (TODO: implement)

#### Request
```
regions
```
or
```
regions <version> <user_id> <password>
```

#### Response
```
{
    "size": <size>
    "files": [
        [<file_1_md5>, <file_1_size>, <file_1_relpath>],
        [<file_2_md5>, <file_2_size>, <file_2_relpath>],
        ...
        [<file_n_md5>, <file_n_size>, <file_n_relpath>]
    ]
}
```

#### Request
```
[
    [<file_1_md5>, <file_1_size>, <file_1_relpath>],
    [<file_2_md5>, <file_2_size>, <file_2_relpath>],
    ...
    [<file_n_md5>, <file_n_size>, <file_n_relpath>]
]
```

#### Response
```
<file_1_data>
<file_2_data>
...
<file_n_data>
```


## Save
Pushes a save to the server. (TODO: implement)

#### Request
```
save <version> <user_id> <password>
```

#### Response
```
ok
```

#### Request
```
<file_count>
```

#### Response
```
ok
```

#### Request
```
[  
    <region_name>,  
    <city_1_name>  
]
```

#### Response
```
ok
```

#### Request
```
<data>
```

#### Response
```
ok
```

#### Request
```
[  
    <region_name>,  
    <city_2_name>  
]
```

#### Response
```
ok
```

#### Request
```
<data>
```

#### Response
```
ok
```

...

#### Request
```
[  
    <region_name>,  
    <city_n_name>  
]
```

#### Response
```
ok
```

#### Request
```
<data>
```

#### Response
```
<message>
```


## Server description
Returns the server description.

#### Request
```
server_description
```

#### Response
```
<server_description>
```


## Server ID
Returns the server ID.

#### Request
```
server_id
```

#### Response
```
<server_id>
```


## Server list
Returns the server list in a 2d JSON array.

#### Request
```
server_list
```

#### Response
```
[  
    [<server_1_host>, <server_1_port>],  
    [<server_2_host>, <server_2_port>],  
    ...  
    [<server_n_host>, <server_n_port>]  
]  
```


## Server name
Returns the server name.

#### Request
```
server_name
```

#### Response
```
<server_name>
```


## Server URL
Returns the server URL.

#### Request
```
server_url
```

#### Response
```
<server_url>
```


## Server version
Returns the version of the SC4MP Server that the server is running on.

#### Request
```
server_version
```

#### Response
```
<server_version as major.minor.patch>
```


## Time
Returns the time in the server's timezone.

#### Request
```
time
```

#### Response
```
<time as Y-m-d H:M:S>
```


## Token
Returns a radomized token that is used for server verification.

#### Request
```
token <version> <user_id> <password>
```

#### Response
```
<token>
```


## User ID
Returns a user_id from an SHA-256 hash of a concatenation of the user_id and client-side token. Used to verify that the server has the user ID on record.

#### Request
```
user_id <hash>
```

#### Response
```
<user_id>
```


## User plugins enabled
Returns "y" if user plugins are permitted, otherwise "n".

#### Request
```
user_plugins_enabled
```

#### Response
```
y
```
or
```
n
```