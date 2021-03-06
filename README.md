# Nagato
WIP Discord bot written in golang using [Discordgo](https://github.com/bwmarrin/discordgo).

# Progress / TODO
See [TODO](https://github.com/chaseweaver/Nagato/blob/master/TODO.md)

# Info
This project was started as a more-modular based approach to handle commands and events.
As such, each command has a properties file as well as a func that is called.
Example and templates are shown below.

# Prerequisites
1. Follow this [Effective Go](https://golang.org/doc/effective_go.html?)
2. And this [Documenting Go Code](https://blog.golang.org/godoc-documenting-go-code)
3. **Create a REDIS server.**

# Install / Run
1. Clone this repo
    ```
    git clone https://github.com/chaseweaver/Nagato.git
    ```
2. Install required dependencies
    * Follow the install for the developer branch of [Discordgo](https://github.com/bwmarrin/discordgo)
    * Also install [gonfig](https://github.com/Tkanos/gonfig) using the same process.
    * And again [redigo](https://github.com/gomodule/redigo)
    * And again again [go-cache](https://github.com/patrickmn/go-cache)
3. Rename `config.ex.json` to `config.json`
4. Register a bot account at [Discord App Developers](https://discordapp.com/developers/docs/intro)
5. Grab bot `Token` and paste it in the newly renamed `config.json` file.
6. Build the project 
    ```go
    $ go build
    ```
7. Run the bot
    ```go
    $ ./Nagato
    ```
8. ezpz

# Adding Bot to a Guild
1. Go back to [Discord App Developers's](https://discordapp.com/developers/docs/intro)
2. Grab `Client ID`
3. Go to [Discord Permissions Calculator](https://discordapi.com/permissions.html) and select the required permissions and paste your `Client ID` in.
4. Click on newly-creted link.
5. ezpz

# Templates
* init (to be placed in `func init() { ... }`)
    ```go
    func init() {
        RegisterNewCommand(Command{
            Name:            "command name",
            Func:            FunctionName,
            Enabled:         true,
            NSFWOnly:        false,
            IgnoreSelf:      true,
            IgnoreBots:      true,
            Cooldown:        30,
            RunIn:           []string{"Text", "DM"},
            Aliases:         []string{"nameone", "nametwo"},
            UserPermissions: []string{"Kick Members"},
            ArgsDelim:       " ",
            Usage:           []string{"<@Member>", "Other"},
            Description:     "Description Here",
        })

        // RegisterNewCommand(Command{ ...
    }
    ```

* Commands (to be placed in the desired `*.go`)
  ```go
  func CommandName(ctx Context) {
	  // Do some neat things here
	  return
  }
  ```

* Events (to be placed in `events.go`)
    ```go
    func EventName(ctx Context) {
      // More neat stuff
    }
    ```

# Command Properties
Each command has it's own properties that dictate when / how it can be run.
Here's the list of currently supported properties:

### Command
This is to be passed in for each func call:

| Property        | Description                                                          | Type                                                   |
| --------------- |----------------------------------------------------------------------| -------------------------------------------------------|
| Name            | Name of the command, case sensitive                                  | [string](https://golang.org/pkg/builtin/#string)       |
| Func            | Name of the command func that gets ran, case sensitive               | func                                                   |
| Enabled         | Whether or not the command is enabled and can be ran                 | [bool](https://golang.org/pkg/builtin/#bool)           |
| NSFWOnly        | Whether or not the command is only available in NSFW-marked channels | [bool](https://golang.org/pkg/builtin/#bool)           |
| IgnoreSelf      | Whether or not the bot will ignore itself                            | [bool](https://golang.org/pkg/builtin/#bool)           |
| IgnoreBots      | Whether or not the bot will ignore other bots                        | [bool](https://golang.org/pkg/builtin/#bool)           |
| Cooldown        | Time the command can be ran again by the same user                   | [int](https://golang.org/pkg/builtin/#int)           |
| RunIn           | Channel type the command can be ran in (DM, Text)                    | [\[\]string{}](https://golang.org/pkg/builtin/#string) |
| Aliases         | Other names the command will execute under                           | [\[\]string{}](https://golang.org/pkg/builtin/#string) |
| UserPermissions | Permissions the user needs in order for the command to execute       | [\[\]string{}](https://golang.org/pkg/builtin/#string) |
| ArgsDelim       | Seperator that will parse individual arguments                       | [string](https://golang.org/pkg/builtin/#string)       |
| Usage           | Example of how to run the command, used for `help`                   | [\[\]string{}](https://golang.org/pkg/builtin/#string) |
| Description     | Description of the command, used for `help`                          | [string](https://golang.org/pkg/builtin/#string)       |


### Context
This is to be passed in for each func call:

| Property | Description                         | Type                                                                   |
| -------- |-------------------------------------| -----------------------------------------------------------------------|
| Session  | *discordgo.Session                  | [Session](https://godoc.org/github.com/bwmarrin/discordgo#Session)     |
| Event    | *discordgo.MessageCreate            | [Event](https://godoc.org/github.com/bwmarrin/discordgo#MessageCreate) |
| Guild    | *discordgo.Guild                    | [Guild](https://godoc.org/github.com/bwmarrin/discordgo#Guild)         |
| Channel  | *discordgo.Channel                  | [Channel](https://godoc.org/github.com/bwmarrin/discordgo#Channel)     |
| Command  | Command to be run                   | [Command](https://github.com/chaseweaver/Nagato#command)               |                                                    |
| Name     | Name of the command, case sensitive | [string](https://golang.org/pkg/builtin/#string)                       |
| Args     | Arguments passed in for the command | [\[\]string{}](https://golang.org/pkg/builtin/#string)                 |

### UserPermissions
Permissions the Author of the command needs in order for the bot to run said command (really only need the important ones like KickMembers, etc).

* Bot Owner (bot owner, forces all commands to run regardless)
* Read Messages
* Send Messages
* Send TTS Messages
* Manage Messages
* Embed Links
* Attach Files
* Read Message History
* Mention Everyone
* Use External Emojis
* Voice Connect
* Voice Speak
* Voice Mute Members
* Voice Deafen Members
* Voice Move Members
* Voice Use VAD
* Change Nickname
* Manage Nicknames
* Manage Roles
* Manage Webhooks
* Manage Emojis
* Create Instant Invite
* Kick Members
* Ban Members
* Administrator
* Manage Channels
* Manage Server
* Add Reactions
* View Audit Logs
* All Text
* All Voice
* All Channel
* All