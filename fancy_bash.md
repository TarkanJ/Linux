# Regular Colors

| Value    | Color  |
| -------- | ------ |
| \e[0;30m | Black  |
| \e[0;31m | Red    |
| \e[0;32m | Green  |
| \e[0;33m | Yellow |
| \e[0;34m | Blue   |
| \e[0;35m | Purple |
| \e[0;36m | Cyan   |
| \e[0;37m | White  |

```bash
# This lines add at the bottom in ~/.bashrc

# Source global definitions
# MARTINO fancy color BASH ;o)
# @2026
if [ -f /etc/bashrc ]; then
        . /etc/bashrc
fi
PS1='\[\033[1;96m\]\u\[\033[1;34m\]@\[\033[1;35m\]\h\[\033[1;34m\]:\[\033[1;36m\]\w\[\033[1;32m\]\$\[\033[0m\] '
# PS1='\[\033[1;36m\]\u\[\033[1;31m\]@\[\033[1;32m\]\h:\[\033[1;35m\]\w\[\033[1;31m\]\$\[\033[0m\] '
export PATH=$HOME/local/bin:$PATH
```

• Name (\u - cyan/light cyan): \033[1;96m (light cyan/cyan)

• At sign (@ - purple-blue): \033[1;34m (blue) or purple \033[1;35m (choose according to your preference)

• Host/computer (\h - purple-blue): \033[1;95m (bright purple/magenta)

• Colon (: - blue): \033[1;34m (blue)

• Path (\w - light cyan): \033[1;36m (cyan)

• Dollar sign (\$ - bright red): \033[1;91m (bright/vivid red)

• Reset (\033[0m): Returns the color to the default state.
