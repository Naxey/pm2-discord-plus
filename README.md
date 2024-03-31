# pm2-discord-plus

This is an improved PM2 Module for sending events & logs from your PM2 processes to Discord.

## Install

To install and setup pm2-discord-plus, run the following commands:

```text
pm2 install pm2-discord-plus
pm2 set pm2-discord-plus:discord_url https://discord_url
```

### Where do I find the `discord_url`?

To get the Discord URL, you need to setup a Webhook. More details on how to set this up can be found here: <https://support.discordapp.com/hc/en-us/articles/228383668-Intro-to-Webhooks>

## Configure

The following events can be subscribed to:

- **log** - All standard out logs from your processes. `Default: true`
- **error** - All error logs from your processes. `Default: false`
- **kill** - Event fired when PM2 is killed. `Default: true`
- **exception** - Any exceptions from your processes. `Default: true`
- **restart** - Event fired when a process is restarted. `Default: false`
- **delete** - Event fired when a process is removed from PM2. `Default: false`
- **stop** - Event fired when a process is stopped. `Default: true`
- **restart overlimit** - Event fired when a process is reaches the max amount of times it can restart. `Default: true`
- **exit** - Event fired when a process is exited. `Default: false`
- **start** - Event fired when a process is started. `Default: false`
- **online** - Event fired when a process is online. `Default: false`

You can simply turn these on and off by setting them to true or false using the PM2 set command.

```text
pm2 set pm2-discord-plus:log true
pm2 set pm2-discord-plus:error false
...
```

## Options

The following options are available:

- **process_name** (string) When this is set, it will only output the logs of a specific named process `Default: NULL`
- **buffer** (bool) - Enable/Disable buffering of messages by timestamp. Messages that occur with the same timestamp (seconds) will be concatenated together and posted as a single discord message. `Default: true`
- **buffer_seconds** (int) - Duration in seconds to aggregate messages. Has no effect if buffer is set to false. `Min: 1, Max: 5, Default: 1`
- **queue_max** (int) - Number of messages to keep queued before the queue will be truncated. When the queue exceeds this maximum, a rate limit message will be posted to discord. `Min: 10, Max: 100, Default: 100`

Set these options in the same way you subscribe to events.

Example: The following configuration options will enable message buffering, and set the buffer duration to 2 seconds. All messages that occur within 2 seconds of each other (for the same event) will be concatenated into a single discord message.

```text
pm2 set pm2-discord-plus:process_name myprocess
pm2 set pm2-discord-plus:buffer true
pm2 set pm2-discord-plus:buffer_seconds 2
pm2 set pm2-discord-plus:queue_max 50
```

## Contributing

In lieu of a formal styleguide, take care to maintain the existing coding style. Add unit tests for any new or changed functionality. Lint and test your code.

## Acknowledgements

Forked from [FranciscoG/pm2-discord](https://github.com/FranciscoG/pm2-discord) for quality of life improvements.
