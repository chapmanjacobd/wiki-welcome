# wiki-welcome

![](preview.gif)

A welcome banner for your shell which selects a few lines from a random Wikipedia article.

I included some 800 random Level-5 Vital Wikipedia articles so the topics won't be too unimportant.

## To install:

### Fish

```fish
function fish_greeting
    cat /proc/loadavg | cut -d' ' -f 2
    set article (/usr/bin/ls -p  ~/placedata/wikipedia_text/ |grep -v / | shuf -n 1)
    set_color -o -u
    echo (string replace '_' ' ' (string replace '.txt' '' (string unescape --style=url $article))) | sed 's/.*/\L&/; s/[a-z]*/\u&/g' | sed -E 's/ (The|A|Of|I[sn]|For)\b/\L&/g'
    set_color normal
    head -7 ~/placedata/wikipedia_text/$article | cowthink -W 78 -f tux
end
```

Alternatively, for more randomness you can change `head` to `shuf` like this:

```sh
shuf -n7 ~/placedata/wikipedia_text/$article | cowthink -W 78 -f tux
```

PRs are welcome--except for adding more wikipedia articles. I can add all Level-5 Vital articles just fine but it is over 1GB so...
