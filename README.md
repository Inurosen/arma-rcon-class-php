# Arma RCon Class for PHP (ARC)

ARC is a lightweight PHP class, which let's you easily send commands via  RCon to your Arma server. See "Supported Server" for a full list of supported Arma games.
<br>
<br>
## Supported Servers
Please consider that mods normally don't change the BattlEye server settings, so this class also works for sending RCON commands  to servers running mods (e.g Altis Life, DayZ, Epoch etc.).

| App ID        | Game          | RCON Support       |
|---------------|---------------|:------------------:|
|233780         | Arma 3        | :white_check_mark: |
|33935          | Arma 2: Operation Arrowhead       | :white_check_mark: |
|33905          | Arma 2        | :white_check_mark: |
<br>
## Requirements
ARC only requires **PHP5**, nothing more!
<br>
<br>
## Installation
To use ARC in your project, just inlcude `rcon.php` in your project.
```php
require_once '{PATH_TO_RCON.PHP}/rcon.php';
```
<br>
## Examples
#### Getting started
After including `rcon.php` in your project, you need to create a new object, e.g:
```php
$rcon = new \Nizarii\ARC("Your server IP", Port, "RCon password");
```
Then you are able to send commands with the `command()` function:
```php
$rcon->command("Say -1 hello!"); // To say something in global chat, you may use 'say_global()', see 'Functions'
```
ARC will throw Exceptions if anything goes wrong, so you could do a try-catch function:
```php
try 
{
    $rcon = new \Nizarii\ARC("Your server IP", Port, "RCon password");
    $rcon->say_player(0, "hey!");
} 
catch (Exception $e) 
{
    echo "Ups! Something went wrong: ".$e->getMessage();
}
```
#### Options
ARC can send a heartbeat packet to the server. In order to do this, you need to enable it:
```php
$rcon = new \Nizarii\ARC("Your server IP", Port, "RCon password", array (
        'heartbeat' => true,
    ));
```
Another option is `timeout_seconds`, which sets a timeout value on the connection:
```php
$rcon = new \Nizarii\ARC("Your server IP", Port, "RCon password", array (
        'send_heartbeat'       => true,
        'timeout_seconds'      => 1, // by default 1 second
    ));
    
$rcon->write_bans(); 
```
<br>
## Functions
ARC features many functions to send BattlEye commands easier:
* `command()`:  Sends any command to the BattlEye server and returns its answer as a string.
* `kick_player($player)`:  Kicks a player who is currently on the server.
* `get_players()`:  Returns a list of all players online.
* `say_global($message)`:  Sends a global message to all players.
* `say_player($player, $message)`:  Sends a message to a specific player.
* `get_missions()`:  Returns a list of the available missions on the server.
* `load_scripts()`:  Loads the "scripts.txt" file without the need to restart the server.
* `max_ping($ping)`:  Changes the MaxPing value. If a player has a higher ping, he will be kicked from the server.
* `change_password($password)`:  Changes the RCon password.
* `load_bans()`:  (Re)load the BE ban list from bans.txt.
* `get_bans()`:  Show a list of all BE server bans.
* `ban_player($player, $reason, $time)`:  Ban a player's BE GUID from the server. If time is not specified or 0, the ban will be permanent; if reason is not specified the player will be kicked with "Banned".
* `add_ban($player, $reason, $time)`:  Same as "ban_player", but allows to ban a player that is not currently on the server.
* `remove_ban($banid)`:  Removes a ban.
* `write_bans()`:  Removes expired bans from bans file.
* `disconnect()`:  Closes the connection to the BattlEye server manually, sending commands after calling this function is not possible
* `connect()`:  Creates a new connection to a server, please remind to close the connection before using this function

*See [here](https://community.bistudio.com/wiki/BattlEye "BattlEye Wiki") for more information about BattlEye*
<br>
<br>
## License

The MIT License (MIT)

Copyright (c) 2015 Felix Schäfer

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
