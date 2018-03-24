# zsh

## 常用配置
|参数|含义|
|:---|:---|
|%n|username|
|%m|hostname(truncated to the first period)|
|%M|full hostname|
|%?|return code of the last-run application|
|%#|The prompt based on user privileges|
|%T|System time(HH:MM)|
|%*|System time(HH:MM:SS)|
|%D|System date(YY-MM-DD)|
|%~|current working directory|
|%d|The current working directory|
常用配置
> export PS1="\${ret_status} %{\$fg[blue]%}[%D{%Y-%m-%d %I:%M:%S}] %{\$fg[green]%}%n@%M %{\$fg[cyan]%}%~%{\$reset_color%} \$(git_prompt_info)
\> "

[返回目录](../CONTENTS.md)