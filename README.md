# wiki-welcome

This repo uses material from Wikipedia, which is released under the <a href="https://creativecommons.org/licenses/by-sa/3.0/">Creative Commons Attribution-Share-Alike License 3.0</a>. Respective authorship can be found on the page of each article.

![](preview.gif)

A welcome banner for your shell which selects a few lines from a random Wikipedia article.

I include all [Level-5 Vital Wikipedia articles](https://en.wikipedia.org/wiki/Wikipedia:Vital_articles/Level/5) so the topics won't be unimportant.

## To install:

```
git clone --depth=1 https://github.com/chapmanjacobd/wiki-welcome/ ~/bin/wiki-welcome/
```

### Fish

```fish
function fish_greeting
    cat /proc/loadavg | cut -d' ' -f 2
    set article (/usr/bin/ls -p  ~/bin/wiki-welcome/articles/ |grep -v / | shuf -n 1)
    set articleURL (string replace '.txt' '' $article)
    set_color -o -u
    echo (string replace '_' ' ' (string unescape --style=url $articleURL)) | sed 's/.*/\L&/; s/[a-z]*/\u&/g' | sed -E 's/ (The|A|Of|I[sn]|For)\b/\L&/g'
    echo "https://en.wikipedia.org/wiki/$articleURL"
    set_color normal
    head -c500 ~/bin/wiki-welcome/articles/$article | cowthink -W 78 -f tux
end
```

Alternatively, for more randomness you can change `head` to `shuf` like this:

```sh
shuf -n7 ~/bin/wiki-welcome/articles/$article | cowthink -W 78 -f tux
```


PRs are welcome. Originally I only had a random 800 articles but following a tip from `@_WaylonWalker` I found that I could include all 32,000 articles if I only include the top 500 words. Originally this would have required 1300MB which is far too big but now it is only 139MB.
