# Mac

Mac is a script to set up macOS for web development.

It can be run multiple times safely on the same machine. It installs and
upgrades packages based on what is already installed.

## Requirements

* macOS Sonoma (14.x) on Apple Silicon and Intel
* macOS Ventura (13.x) on Apple Silicon and Intel
* macOS Monterey (12.x) on Apple Silicon and Intel

## Install

Download the script:

```sh
curl --remote-name https://raw.githubusercontent.com/fernandoaleman/mac/master/mac
```

Run the script:

```sh
sh mac 2>&1 | tee ~/mac.log
```

Optionally, review the log:

```sh
less ~/mac.log
```

## Debugging

Your last `mac` run will be saved to `~/mac.log`. Read through it and see if
you can find the issue. If not, open a [new GitHub
Issue](https://github.com/fernandoaleman/mac/issues/new) and attach the log file
as an attachment.

## What This Script Sets Up

macOS tools:

* [Homebrew] for managing operating system libraries.
* [asdf] for managing runtime versions.

[Homebrew]: http://brew.sh/
[asdf]: https://asdf-vm.com

Unix tools:

* [Git] for version control
* [OpenSSL] for Transport Layer Security (TLS)
* [RCM] for managing company and personal dotfiles
* [Tmux] for saving project state and switching between projects
* [Fish] as your default shell

[Git]: https://git-scm.com/
[OpenSSL]: https://www.openssl.org/
[RCM]: https://github.com/thoughtbot/rcm
[Tmux]: https://tmux.github.io/
[Fish]: https://www.fishshell.com/

GitHub tools:

* [GitHub CLI] for interacting with the GitHub API

[GitHub CLI]: https://cli.github.com/

## Customizations

You can add your own customizations by adding them to your `~/.mac.local`
file, which is run at the end of the mac script.

Put your customizations there.
For example:

```sh
#!/bin/sh

brew bundle --file=- <<EOF
brew "go"
EOF

fancy_echo "Cleaning up old Homebrew packages ..."
brew cleanup
```

Make sure your customizations can be run safely more than once.
See the `mac` script for examples.

## Testing

Follow shell style guidelines by using [ShellCheck].

```sh
brew install shellcheck
```

[ShellCheck]: https://www.shellcheck.net/about.html

Test `mac` script

```sh
shellcheck mac
```

Test customizations script

```sh
shellcheck ~/.mac.local
```
