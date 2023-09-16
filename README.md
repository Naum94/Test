# Linux cheatsheet
## BASH Customizations

Colors
```bash
RED="\[\e[1;31m\]";
GREEN="\[\e[1;32m\]";
YELLOW="\[\e[1;33m\]";
BLUE="\[\e[1;34m\]";
PURPLE="\[\e[1;35m\]"; 
AQUA="\[\e[1;36m\]";
WHITE="\[\e[1;37m\]";
RESET="\[\e[0m\]";
```

BASH Prompt example
```bash
PS1="${GREEN}\u${WHITE}@${RED}\h ${WHITE}in ${AQUA}\w ${WHITE}> ${RESET}";
```

Aliases
```bash
alias grep='grep --color=auto'
alias nano='nano -ic'
```
