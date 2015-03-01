# sexy-bash-prompt 
Forked from https://github.com/twolfson/sexy-bash-prompt for my own preferences. The only change so far is to replace the user ID and hostname in the prompt with the docker workspace name.

[Bash][bash] prompt with colors, git statuses, and git branches.

Providing a unique symbol for every combination of a dirty, unpulled, and unpushed `git` branch. (not all are shown)

![sexy-bash-prompt screenshot][screenshot]

[screenshot]: screenshot.png

## Installation
One line install:

```bash
(cd /tmp && git clone --depth 1 https://github.com/ehacke/sexy-bash-prompt && cd sexy-bash-prompt && make install) && source ~/.bashrc
```

## Configuration
### Colors
Colors can be customized by editing `.bash_prompt` directly, or by setting the following environment variables:

- `PROMPT_USER_COLOR` - Color for username (e.g. `todd`)
- `PROMPT_PREPOSITION_COLOR` - Color for 'at', 'in', 'on'
- `PROMPT_DEVICE_COLOR` - Color for machine name (e.g. `Euclid`)
- `PROMPT_DIR_COLOR` - Color for directory (e.g. `~/github/sexy-bash-prompt`)
- `PROMPT_GIT_STATUS_COLOR` - Color for git branch and symbol (e.g. `master`)
- `PROMPT_GIT_PROGRESS_COLOR` - Color for in progress git actions (e.g. `[merge]`)
- `PROMPT_SYMBOL_COLOR` - Color for prompt symbol (e.g. `$`)

You can set colors via [`tput`][] or [ANSI escape codes][]. For example:

[`tput`]: http://en.wikipedia.org/wiki/Tput
[ANSI escape codes]: http://en.wikipedia.org/wiki/ANSI_escape_code

```bash
# Inside your `.bashrc` or `.bash_profile`
PROMPT_USER_COLOR="$(tput bold)$(tput setaf 9)" # BOLD RED
source ~/.bash_prompt
```

![Color overridden prompt](docs/color_override.png)

### Symbols
Similarly, symbols can be customized with the following environment variables:

- `PROMPT_SYNCED_SYMBOL` - Symbol for clean and synced branch (e.g. empty string)
- `PROMPT_DIRTY_SYNCED_SYMBOL` - Symbol for dirty and synced branch (e.g. `*`)
- `PROMPT_UNPUSHED_SYMBOL` - Symbol for unpushed branch (e.g. `△`)
- `PROMPT_DIRTY_UNPUSHED_SYMBOL` - Symbol for dirty and unpushed branch (e.g. `▲`)
- `PROMPT_UNPULLED_SYMBOL` - Symbol for unpulled branch (e.g. `▽`)
- `PROMPT_DIRTY_UNPULLED_SYMBOL` - Symbol for dirty and unpulled branch (e.g. `▼`)
- `PROMPT_UNPUSHED_UNPULLED_SYMBOL` - Symbol for dirty and unpulled branch (e.g. `⬡`)
- `PROMPT_DIRTY_UNPUSHED_UNPULLED_SYMBOL` - Symbol for dirty, unpushed, and unpulled branch (e.g. `⬢`)

```bash
# Inside your `.bashrc` or `.bash_profile`
PROMPT_UNPUSHED_SYMBOL="↑"
source ~/.bash_prompt
```

![Symbol overridden prompt](docs/symbol_override.png)

#### Compatibility
In some situations, the default symbol set can be drawn incorrectly (e.g. as diamonds). To remedy that, a simpler set of symbols can be used:

```bash
PROMPT_SYNCED_SYMBOL=""
PROMPT_DIRTY_SYNCED_SYMBOL="*"
PROMPT_UNPUSHED_SYMBOL="↑"
PROMPT_DIRTY_UNPUSHED_SYMBOL="*↑"
PROMPT_UNPULLED_SYMBOL="↓"
PROMPT_DIRTY_UNPULLED_SYMBOL="*↓"
PROMPT_UNPUSHED_UNPULLED_SYMBOL="*↑↓"
PROMPT_DIRTY_UNPUSHED_UNPULLED_SYMBOL="*↑↓"
```

## How does it work?
[bash][bash] provides a special set of [variables for your prompts][ps-vars]. `PS1` is the one used by default. The install script adds a command to `~/.bashrc`, a file that is run every time a new terminal opens. Inside of the new command, we run our script and set your `PS1` which runs some `git` commands to determine its current state and outputs them as a string.

[bash]: https://en.wikipedia.org/wiki/Bash_%28Unix_shell%29
[ps-vars]: http://www.gnu.org/software/bash/manual/bashref.html#index-PS1

## Support
Linux and Mac OSX are supported platforms.

Windows is supported to the best of my abilities. However, there have been [font issues][putty-issue] with using [PuTTY][].

[PuTTY]: http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html
[putty-issue]: https://github.com/twolfson/sexy-bash-prompt/issues/7

## Contributing
In lieu of a formal styleguide, take care to maintain the existing coding style. Add unit tests for any new or changed functionality. Test via `make test`.

## License
Copyright (c) 2013 Todd Wolfson

Licensed under the MIT license.
