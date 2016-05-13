# fail2ban xmpp action

An action that lets you send xmpp messages.

# Usage

## Prerequisites

The actual send job is delegated to `sendxmpp`.

Installation on debian:

    # apt install sendxmpp

## Preparation

`sendxmpp` itself needs a resource file which holds the account information of the sender:

    fail2ban@my-xmpp-server.net my-secret-password

Don't forget to protect the file after creation:

    # chmod 600 .sendxmpprc

## Installation

Just copy the action file into your `actions.d` folder:

    # cp xmpp.conf /etc/fail2ban/actions.d

## Configuration

Here is an example configuration in the `jail.local`:

```ini
[DEFAULT]
destxmpp = your-account@jabber.de
xmpprcfile = /root/.sendxmpprc

[sshd]
port    = ssh
logpath = %(sshd_log)s
action  = xmpp[destxmpp="%(destxmpp)s", rcfile="%(xmpprcfile)s", name=%(__name__)s, bantime="%(bantime)s"]
```

You need to define two values:

- `destxmpp`: this is the receving xmpp account
- `xmpprcfile`: the path to your prepared sendxmpp resource file