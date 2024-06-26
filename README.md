# CTF 附件收集者

> 群是加的，名是报的，附件是下载的，比赛是爆零的。

这是一个自用小工具，用于批量下载归档 CTF 单场比赛的附件，在开始参赛时和快结束时都很好用。

已支持自定义文件路径模板、赛题方向、最大文件大小、文件覆盖。

对于动态附件，只支持下载已登录用户的附件。

目前支持 GZ::CTF 平台，考虑后续添加其他平台。

⚠ 注意：目前缺乏测试，请谨慎使用。

欢迎 Pull Request。

## 说明

工具的正常工作需要获取必需的用户令牌等信息，这些信息会在程序运行结束时立即丢弃，不会传输到除原比赛平台外的任何位置。

工具有意只同时下载一个文件，以免对平台服务器（更可能是用户 IP 与平台的连通性）造成影响。一般情况下这就足够了。

为避免滥用，不会提供用于练习平台的批量下载功能。一次只能下载一场比赛。

## 使用方法

### GZ::CTF 平台

（本文档已重写以下内容）

``` plain
usage: gzctf_attachment_downloader.py [-h] [-u URL] [-t TOKEN]
                                      [-d ROOT_DIRECTORY]
                                      [-f FILE_PATH] [-k] [-s MAX_SIZE]
                                      [-o] [-E] [-mcpwr] [--blockchain]
                                      [--forensics] [--hardware]
                                      [--mobile] [--ppc] [--ai]

可选项：
  -h, --help            显示帮助信息并退出
  -u URL, --url URL     GZ::CTF 比赛地址，例如
                        https://example.com/games/1/challenges 或者
                        https://example.com/games/1
  -t TOKEN, --token TOKEN
                        Cookie GZCTF_TOKEN 的值
  -d ROOT_DIRECTORY, --root-directory ROOT_DIRECTORY
                        默认是 `pwd`/{game}，这样可以得到 "./LRCTF 2024"
  -f FILE_PATH, --file-path FILE_PATH
                        文件路径格式，默认是 {tag}/{chall}/{origin}，
                        这样可以得到 "misc/sign in/attachment_deadbeef.zip"，
                        以 {origin} 结尾才能保留扩展名
  -k, --keep-spaces     如果指定，"--file-path" 中的空格就不会被替换为 '-'
  -s MAX_SIZE, --max-size MAX_SIZE
                        最大文件大小，以 MB 计，超过的文件会被跳过，
                        默认是 50.0，设为 0 可禁用
  -o, --overwrite       如果指定，已有的文件将被覆盖，而不是跳过

格式化字符串模板说明：
  {game}    从平台接收到的比赛标题，例如 "LRCTF 2024"
  {tag}     小写的赛题方向，例如 "misc"
  {chall}   从平台接收到的赛题名称，例如 "sign in"
  {origin}  从服务器接收到的文件名，例如 "attachment_deadbeef.zip"

标签（方向）选项，默认是全部，可以像 -mwp 这样指定：
  -E, --except-mode     例如 -p 将只下载 pwn，而 -E -p 将除了 pwn 其他都下载
  -m, --misc
  -c, --crypto
  -p, --pwn
  -w, --web
  -r, --reverse
  --blockchain, --forensics, --hardware, --mobile, --ppc, --ai
```

作者自己用的时候，通常不指定任何选项，然后在标准输入中再提供地址和 token。
