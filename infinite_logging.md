# Infinite logging

Logging all commands run in the terminal to file, in  a hidden directory at `~/.logs/`.

In regular bash, popping this wee script (provided by James Ferguson: https://github.com/Psy-Fer) into my ~/.bashrc file worked great, as long as the `~/.logs/` dir existed.

```bash
export PROMPT_COMMAND='if [ "$(id -u)" -ne 0 ]; then echo "$(date "+%Y-%m-%d.%H:%M:%S") $(pwd) $(history 1)" >> ~/.logs/bash-history-$(date "+%Y-%m-%d").log; fi'
```

Example log file:

```bash
bash-3.2$ cat ~/.logs/bash-history-2023-04-17.log 
2023-04-17.18:30:41 /Users/leahkemp/garvan/script_nibs    31  cat ~/.logs/bash-history-2023-04-17.log 
2023-04-17.18:30:44 /Users/leahkemp/garvan/script_nibs    32  balh
2023-04-17.18:30:46 /Users/leahkemp/garvan/script_nibs    33  test
2023-04-17.18:30:48 /Users/leahkemp/garvan/script_nibs    34  blah
```

I've transitioned to working on a mac (macOS Ventura) which uses zsh as the default shell. So I needed to update a few things. First I needed to utilise ~/.zshrc file in place of a ~/.bashrc file. Secondly, I updated my infinite logging script to the following:

```zsh
function precmd() {

if [ "$(id -u)" -ne 0 ]; then echo "$(date "+%Y-%m-%d.%H:%M:%S") $(pwd) $(history -1)" >> ~/.logs/zsh-history-$(date "+%Y-%m-%d").log; fi

}
```

Example log file:

```zsh
leahkemp@Leahs-MacBook-Pro script_nibs % cat ~/.logs/zsh-history-2023-04-17.log 
2023-04-17.18:01:50 /Users/leahkemp  1027  mkdir ~/.logs
2023-04-17.18:01:55 /Users/leahkemp  1028  blah
2023-04-17.18:02:03 /Users/leahkemp  1029  cat ~/.logs/zsh-history-2023-04-17.log 
2023-04-17.18:02:09 /Users/leahkemp  1030  test
2023-04-17.18:02:09 /Users/leahkemp  1031  cat ~/.logs/zsh-history-2023-04-17.log 
```

Note. that I have both a ~/.bashrc and a ~/.zshrc file with the above commands. This means that when I pop into a bash shell, those bash commands will be logged to a file in ~/.logs/ named "bash-history-.........." separate from my zsh ones at "zsh-history-.........."
