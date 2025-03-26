https://hansvlss.top/post/bpb/

BPB Panel 是一个结合 Cloudflare Workers 和 Pages 的代理面板项目，可以帮助用户轻松搭建免费 VPN，实现永久免费节点订阅，为使用 singbox-core 和 xray-core 的跨平台客户端提供配置。
由于 Cloudflare 官方收紧对 BPB 等项目的审查，如果直接使用源码或者原作者提供的混淆代码，很容易出现 1101 的报错（可能代码中包含敏感关键词、或者使用了与他人相同的混淆代码）。
解决办法是利用未混淆的源码进行自定义加密混淆，从而生成独一无二的混淆代码，成功绕过 Cloudflare 的限制。

一、准备工作

1. GitHub 账号：通过 Github Action 自动同步最新 BPB 源代码，并执行代码混淆。

2. Cloudflare 账号：用于部署 BPB Panel 项目。

3. 域名：建议使用域名（解决 Cloudflare Pages 自带域名被墙的问题）。

二、Github 部署

1. 新建 Github 仓库
		创建一个新的仓库，将 BPB Panel 项目代码同步到该仓库。

2. 配置 Github Actions
		在仓库根目录下创建 .github/workflows 文件夹，并在其中创建 Obfuscate.yml 文件。
		将以下代码粘贴进去

注：此 Action 将在每次 push 到 main 分支和每天凌晨 1 点自动执行，下载最新未混淆的 BPB 源代码（origin.js），并生成混淆后的 `_worker.js` 文件，作为你个人专属的 BPB 代码。

3. 执行 Github Actions
		GitHub 仓库通过Obfuscate.yml 会自动下载最新的 BPB 源代码，并执行混淆
		origin.js：最新未加密的 BPB 源代码
		_worker.js：混淆后的个人专属 BPB 代码

三、Cloudflare 部署

1. 登录 Cloudflare，创建 Pages 部署
		在 Cloudflare 控制台中进入 Workers 和 Pages，选择 Pages 部署。		连接到你的 Github 仓库，选择刚才新建的 BPB 项目仓库，然后点击开始部署。

2. 绑定自定义域名（可选）
		在 Pages 项目的 自定义域选项卡，点击设置自定义域。

3. 设置变量
部署成功后，在 Pages 项目界面点击 设置 -> 变量和机密，添加以下变量：
		UUID：使用 UUID 生成器 随机生成一个新的 UUID。
		PROXYIP：填写代理 IP 地址，可从 随机代理 IP 站点 获取，或使用优选域名（例如 cdn-b100.xn--b6gac.eu.org）。
		TR_PASS：填写一个复杂字符串，作为密码。

4. 绑定 KV 命名空间
		创建 KV:点击左侧存储和数据库，再选择 KV,然后创建一个新的 KV 命名空间   注:名称自定义但不能包含“bpb”
		
		绑定 KV:回到创建的 Pages 界面。点击 设置 -> 【绑定】，点击添加，选择添加 KV 命名空间 注:变量名称只能填写“kv”(小写)

5. 重试部署 Pages
		返回 Pages 项目,找到右侧...,点击重试部署

四、BPB 面板设置

1. 验证部署是否成功
		打开浏览器输入:https://[自定义域名]或者你的项目地址,后面加上/panel,检查是否能正常访问BPB面板

2. 修改 BPB 面板密码
		第一次打开 BPB 面板会提示修改密码,请设置一个复杂密码,避免被盗用

3. 配置 BPB 面板参数
		FakeDNS：设置enable
		Proxy IPs / Domains：填写 IP 或者域名，PROXYIP 获取地址：点击访问
		Clean IPs / Domains：优秀 IP 软件下载【点击下面 Download Scanner】 | 在线优选 IP：点击访问
		TLS 端口：需要使用的端口打勾就可以，默认是 443 端口
		ROUTING RULES：Bypass xxx是指 xxx 不走代理（直连访问）｜ Block xxx是指 xxx 被屏蔽访问（无法访问）
		Bypass LAN：绕过本地局域网
		Block Ads：屏蔽广告网址
		Bypass Iran：绕过伊朗
		Block Porn：屏蔽颜色网站
		Bypass China：绕过中国大陆
		Block QUIC：屏蔽 QUIC 协议
		Bypass Russia：绕过俄罗斯
		CUSTOM RULES：除了上面预设的规则外，你可以在这里自定义一些需要直连（Bypass）和屏蔽（Block）的 IP 地址/网站。

4. 保存设置
		点击 APPLY SETTINGS 保存 BPB 面板配置

五、VPN 节点部署完成

1. 导出节点订阅链接
		根据你所使用的代理软件，点击对应的 COPY SUB 按钮，复制 BPB 面板生成的订阅链接。

现在 BPB 面板 VPN 部署全部结束,通过以上步骤,你可以利用 Cloudflare 和 BPB Panel 搭建一个永久免费 VPN,同时通过对 BPB 源代码进行加密混淆生成专属混淆代码,成功绕过 Cloudflare 的审查,解决 1101 报错问题.



【CF项目详解】

@i域名测试站点：
①cloudns免费:
workers3.0.4:
https://txt.ic666.ddns-ip.net/0808 #web2txt
https://b1.ic666.ddns-ip.net/panel #bpb3混淆版
pages自动化3.1.1:
https://antidana.ic666.ddns-ip.net/panel
https://antidana.pages.dev/panel
内网穿透：
https://f.ic666.ddns-ip.net/files/mnt/sda1/
https://n190.ic666.ddns-ip.net/cgi-bin/luci/ #远程主路由
cloudns官方网站：
https://www.cloudns.net/records/domain/8924641/
帐号：
antidana9@gmail.com/Hh&090909 

②namesilo(付费至202508):
https://test-top.ic666.top/ #test
https://b6.ic666.top/panel #bpb明文自混淆
https://n190file.ic666.top/files/mnt/ #内网穿透

CF隧道管理:
https://one.dash.cloudflare.com/1908f0ae18637940f0a6d2120e4550a1/networks/tunnels

@如果旁路由CF/BPB代理网络下iPad无法访问某些站点，尝试更改WiFi网络设置：
？先忽略此网络再手动加入隐藏网络，轻点“其他”，然后输入网络的名称、安全类型和密码、私有地址（轮替）。
@解决开启CF反代后访问CF项目和某些错误分流问题：
-不要开启绕过中国大陆
-取消禁用QUIC(禁用则cf-tunnels不通）
-更新 GEOIP 数据库、GEOSITE 数据库和大陆白名单
-覆写设置-规则设置-仅代理命中规则流量(取消则cf-tunnels不通）
-自定义规则：
找到 rules 字段（在最上面编辑框内），添加以下规则：
rules:
 - DOMAIN-SUFFIX,cloudflare.com,DIRECT
 - DOMAIN-SUFFIX,apple.com,DIRECT
 - DOMAIN-SUFFIX,ic666.ddns-ip.net,DIRECT
 - DOMAIN-SUFFIX,ic666.ip-ddns.com,DIRECT
 - DOMAIN-SUFFIX,ic666.top,DIRECT 
注意：缩进必须严格对齐，否则会导致 Clash 无法正常运行。

【域名托管教程】
1.登录CF控制台，添加需要托管的域名。会自动扫描可用的DNS记录，如果没有，可以后再添加。
2. 登录原域名服务商账号，将DNS解析改为自定义解析：删除原域名服务解析条目，输入CF提供的两个解析服务器。如果有DNSSEC设置，需要关闭。完成后如：
①主机/ic666.ddns-ip.net；类型/NS；指向到/kai.ns.cloudflare.com
②主机/ic666.ddns-ip.net；类型/NS；指向到/ursula.ns.cloudflare.com
3. 解决重定向问题：如出现网页访问反复重定向问题，需要到SSL/TLS标签下，将模式选为完全（严格）/Full(Strict)即可解决。
4. 双向解析问题：
如免费域名cloudns:
CF默认*、www记录和新增子域名都必须双向解析到cloudns服务器，并在CF-ssl/tls边缘证书设置中复制2个TXT项及值添加到ClouDNS记录中。
-*、www记录填：主机/ic666.ddns-ip.net；类型/NS；指向到/CF自动扫描到的188.165.11.93或PING本域名地址的第一个IP。
-子域名填：
CF:workers添加自定义域名如b3.ic666.ddns-ip.net
对应ClouDNS添加3条记录：
①主机/b3.ic666.ddns-ip.net；类型/CNAME（或A）；指向到:第一个NS记录的值kai.ns.cloudflare.com（或者workers项目名b3.antidanatoritania.workers.dev ！可能不行！）
②主机/_acme-challenge.ic666.ddns-ip.net；类型/ TXT；指向到/ CF复制的值1
③主机/_acme-challenge.b3.ic666.ddns-ip.net；类型/ TXT；指向到/ CF复制的值2

！注意：
①付费域名如Namesilo/ic666.top不需要双向解析
②cloudflare 隧道以及个别项目双向解析之后，可能不需要边缘证书，添加新DNS记录后边缘证书未自动添加到待验证项目，此时不影响域名解析③如果因证书问题解析失败，尝试删除域名后重建以触发证书

5.SSL/TLS设置：
边缘证书：
-自动HTTPS重写
-始终使用HTTPS
-Brotli:应用Brotli压缩，加快访问者的HTTPS流量的页面加载时间。
-源服务器-创建证书，可以申请cloudflare的15年的免费SSL证书。

@DNS解析的Proxied模式与DNS Only模式的区别：
-DNS Only模式下，所有的网络流量都会直接到服务器的实际IP。Cloudflare不会在这个过程中提供任何的安全防护。
-Proxied模式下，所有的网络请求都会进入Cloudflare的IP而不是直接访问服务器的实际IP。Cloudflare会在前端提供安全防护如DDOS。但是在这种模式下，所有的非标准端口就不能工作了。即：浏览器访问（80/443标准端口）能正常工作，但是ssh（非标准端口）就没法连接上。

@问题延伸：
①目前Cf的机制是，用户在域名下增加A/AAAA/CNAME等DNS记录，开启代理，在worker路由中加上这个记录的（子）域名，访问这个（子）域名就会经过worker。所以不开Cf反代就不可能访问上。
？即：workers +自定义域必须走代理，否则通过自定义域名无法进入workers。但是在CF中部暑BPB时，开了反代则进面板有问题，不开反代又无法完成clash节点更新。(已解决：全局自定义规则绕过CF;访问其他CF项目关闭代理即可）
②慎重更改CF自定义域名DNS记录状态为仅DNS，否则打不开面板。仅DNS应该只适用于托管到CF实现CDN和加密，不适于CF中项目。
