You run commands by sending

    !!/commandName [commandArg0, [commandArg1, [...]]]
In a chatroom where the bot is present (cross-room support is planned.)

For example:

    !!/listcommands
Will print something like this:

    @yourUsername Available commands: help, live, die, forget, define, mdn, jquery, online, user, listcommands, get, learn

## `forget`

    !!/forget cmdName

Have the bot forget `cmdName`. You may have to have permission to forget certain commands. Once a command is forgotten, it cannot be un-forgotten (unless, of course, it is `/learn`ed.)

## `define`

    !!/define something

Gives you the definition of `something`. Uses the wonderful [DuckDuckGo api.](http://api.duckduckgo.com/)

## `roll`

    !!/roll [sidesNum] [rollCount]

Rolls a `sidesNum` (default 6) sides die `rollCount` (maximum 100, default 1) times and prints the result.

    roll a 6-sided die 17 times
    !!/roll 6 17
    roll a 3-sided die 1 time
    !!/roll 3
    roll a 6-sided die 1 time
    !!/roll

## `choose`

    !!/choose option0 [, option1 [, option2 [,...]]]

Make the bot choose an option for you.

    !!/choose "go to sleep" "eat food" "do work"
    will result in one of the following, semi-randomly:
    go to sleep
    eat food
    do work

## `tell`

    !!/tell usrName|msgid cmdName [commandArg0, [commandArg1, [...]]]

Executes the command `cmdName`, and have the output be a reply to either a user or a specific message.

    !!/tell Thor listcommands
    !!/tell 253961 mdn Date.parse

    will output something like this:
    @Thor Available commands: help, live, die, forget, define, mdn, jquery, online, user, listcommands, get, learn
    :253961 https://developer.mozilla.org/en/JavaScript/Reference/Global_Objects/Date/parse

**NOTE:** For bot-safety reasons, there are several commands which cannot be executed via `tell`. At the time of writing, they are `tell` and `forget`.

## `get`

    !!/get getterName [range [userid]]

    or, to be more descriptive:
    !!/get answer|question [first|last [userid]]

    The following provide the same result, assuming your userid is 1337:
    !!/get answer
    !!/get answer last 1337
    !!/get answer 1337
    Which is a link to the latest answer by user 1337

### `getterName`
Name of what you wish to get. Valid values are `answer` and `question`.

### `range`
The "range" specifier of what you wish to get. Valid values: `first`, `last` and `between`.

If `between` is specified, then the next two arguments should be the beginning date, and the end date, as such:

    !!/get getterName between "beginning date" "end date" [userid]
Both dates are supposed to be valid strings, which can be parsed by `Date.parse`

### `userid`
The userid of the user from which you wish to get. Defaults to your own.

## `learn`

    !!/learn commandName outputPattern [inputRegex]

    !!/learn greet "Hello, $0!" \w+

### `commandName`
An alphanumeric string

### `outputPattern`
A string, which can contain some special variables:

#### Matched groups
`$0, $1, ..., $n` for the capture-groups you specified in `inputRegex`

#### Filler variables
Special variables (macros) defined by the bot.

* `$who` The name of the user who sent the message
* `$someone` The name of a random, recently active user
* `$digit` A random digit between 0-9

#### Message object variables
Objects used by SO when passing messages around.

* `content` Message content
* `event_type` Speaks for itself - will always be 1 (new message)
* `id` ?
* `message_id` Message ID
* `room_id` Room id
* `room_name` Room name
* `time_stamp` Do I have to explain these?
* `user_id` I mean, they're so obvious,
* `user_name` aren't they?

### `inputRegex`
Like any regular regex, except that instead of where you'd use `\`, you use `~`.
For example: `\w => ~w`, `\\d => ~~d`.

Defaults to `.*`

## `hang`

    !!/hang [guess]

Starts a Hangman game. If there is no game running, calling this command in any form will start a new game. If a game is running, then it accepts a single argument as your guess. Error messages included.
You have 6 guesses to get the word right.

**NOTE:** The hangman game is a more like a module than a core part of the bot. So it may not be available, unless the bot owner explicitly loaded it.

To bot owner: Via your console, simply doing `IO.loadScript( bot.dependencies.hangman )` should automagically get everything imported and done. If you're just using the bookmarklet, you're good to go.

## `todo`

    !!/todo get|add|delete item1|[count [, item2 [...]]]
~TODO~

I'm not very good in writing README files.