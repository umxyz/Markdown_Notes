# [clashx文件规则](clashx文件规则)

使用 clashX Pro 的 `rule-providers` 可以解决

`config.yaml`:

```yaml
rule-providers:
  fy:
    behavior: "classical"
    type: file
    path: ./providers/rules.yaml

rules:
  - RULE-SET,fy,Proxy # 这里的 fy 和上面对应
```

`rules.yaml` 是这样的：

```yaml
payload:
  - DOMAIN-SUFFIX,lin.ee
  - DOMAIN-SUFFIX,line.me
  - DOMAIN-SUFFIX,line.naver.jp
  - DOMAIN-SUFFIX,line-apps.com
  - DOMAIN-SUFFIX,line-cdn.net
  - DOMAIN-SUFFIX,line-scdn.net
  - DOMAIN-KEYWORD,v2ex
  - DOMAIN-SUFFIX,medium.com
  - DOMAIN-SUFFIX,reddit.com
  - DOMAIN-SUFFIX,redditmedia.com
  - DOMAIN-SUFFIX,redd.it
  - DOMAIN-SUFFIX,redditstatic.com
  - DOMAIN-SUFFIX,quora.com
  - DOMAIN-SUFFIX,quoracdn.net
  - DOMAIN-SUFFIX,twimg.com
  - DOMAIN-SUFFIX,twitter.com
  - DOMAIN-SUFFIX,stackoverflow.com
  - DOMAIN-SUFFIX,imgur.com
  - DOMAIN-SUFFIX,spotify.com
  - DOMAIN-SUFFIX,discordapp.net
  - DOMAIN-SUFFIX,discord.com
  - DOMAIN-SUFFIX,cdn.discordapp.com
  - DOMAIN-SUFFIX,github.com
  - DOMAIN-SUFFIX,pornhub.com
  - DOMAIN-SUFFIX,91porn.com
  - DOMAIN-SUFFIX,wikipedia.org
```

这样每次订阅更新的时候，就不会影响自定义 rule 了！

