
Frps服务端一键配置脚本，Frp最新版本：0.61.0
===========

*Frp 是一个高性能的反向代理应用，可以帮助您轻松地进行内网穿透，对外网提供服务，支持 tcp, http, https 等协议类型，并且 web 服务支持根据域名进行路由转发。*

* 详情：fatedier (https://github.com/fatedier/frp)
* 此脚本原作者：clangcn (https://github.com/clangcn/onekey-install-shell)
* foke自：MvsCode (https://raw.githubusercontent.com/MvsCode/frps-onekey/master/install-frps.sh)

## Frps-Onekey-Install-Shell For CentOS/Debian/Ubuntu/Fedora (32bit/64bit)

### Install（安装）
#### Github
ARM
```Bash
wget https://raw.githubusercontent.com/jane77u/frps-onekey/main/install-frps.sh -O ./install-frps.sh
chmod 700 ./install-frps.sh
./install-frps.sh install
```

AMD
```Bash
wget https://raw.githubusercontent.com/jane77u/frps-onekey/main/install-frps_amd.sh -O ./install-frps.sh
chmod 700 ./install-frps.sh
./install-frps.sh install
```

#### Aliyun（已失效）
```Bash
wget https://code.aliyun.com/MvsCode/frps-onekey/raw/master/install-frps.sh -O ./install-frps.sh
chmod 700 ./install-frps.sh
./install-frps.sh install
```

### Uninstall（卸载）
```Bash
./install-frps.sh uninstall
```
### Update（更新）
```Bash
./install-frps.sh update
```
### Server management（服务管理器）
```Bash
Usage: /etc/init.d/frps {start|stop|restart|status|config|version}
```
Frps onkey-install-shell Changelog<br>Frp版本更新说明
---------------------------------------

 <!-- vim-markdown-toc GFM -->
* ## [v0.51.0 [2023/07/05]](#v0.51.0[2023/06/26]https://github.com/fatedier/frp/releases/tag/v0.51.0])
    * ### Features
     > frpc supports connecting to frps via the wss protocol by enabling the configuration protocol = wss.

     > frpc supports stopping the service through the stop command.

    * ### Improvements
     > service.Run supports passing in context.

    * ### Fixes
     > Fix an issue caused by a bug in yamux that prevents wss from working properly in certain plugins.
 
* ## [v0.50.0 [2023/06/26]](#v0.50.0[2023/06/26]https://github.com/fatedier/frp/releases/tag/v0.50.0])
  ##### 为了增强安全性，tls_enable和disable_custom_tls_first_byte的默认值已设置为true。

  如果希望恢复到以前的默认值，则需要手动将这两个参数的值设置为false。

    * ### Features
     > Added support for in stcp, sudp, xtcp. By default, only the same user is allowed to access. Use to allow access from any user. 
     The visitor configuration now supports to connect to proxies of other users.allow_users*server_user

     > Added fallback support to a specified alternative visitor when xtcp connection fails.

    * ### Improvements
     > Increased the default value of MaxStreamWindowSize for yamux to 6MB, improving traffic forwarding rate in high-latency scenarios.

    * ### Fixes
     > Fixed an issue where having proxies with the same name would cause previously working proxies to become ineffective in xtcp.
 
* ## [v0.49.0 [2023/05/29]](#v0.49.0[2023/05/29])
  我们在这个版本中彻底重构了 xtcp，以提高其渗透率和稳定性。

  在此版本中，可以通过多次重试连接来尝试不同的渗透策略。成功打洞后，该策略将记录在服务器缓存中以做将来备用。当新用户连接时，成功穿透的隧道可以重复使用，而不是打新洞。

  ##### 由于 xtcp 的重大重构，此版本与以前版本的 xtcp 不兼容。

  ##### 要使用与xtcp相关的功能，frpc和frps都需要更新到最新版本。
    * ### New
     > The frpc has added the nathole discover command for testing the NAT type of the current network.

     > XTCP has been refactored, resulting in a significant improvement in the success rate of penetration.

     > When verifying passwords, use subtle.ConstantTimeCompare and introduce a certain delay when the password is incorrect.

    * ### Fix
     > Fix the problem of lagging when opening multiple table entries in the frps dashboard.

* ## [v0.48.0 [2023/03/08]](#v0.48.0[2023/03/08])
    * ### New
     > The httpconnect type in tcpmux now supports authentication through the parameters http_user and http_pwd.

    * ### Improved
     > The web framework has been upgraded to vue3 + element-plus, and the dashboard has added some information display and supports dark mode.
     
     > The e2e testing has been switched to ginkgo v2.

* ## [v0.47.0 [2023/02/10]](#v0.47.0[2023/02/10)
    * ### New
     > Added config bandwidth_limit_mode in frpc, default value is client which is current behavior. Optional value is server, to enable bandwidth limit in server. The major aim is to let server plugin has the ability to modify bandwidth limit for each proxy.

    * ### Improve
     > dns_server supports ipv6.

     > frpc supports graceful shutdown for protocol quic.

* ## [v0.46.1 [2023/01/10]](#v0.46.1[2023/01/10])
    * ### Fix
     > Server Plugin sends incorrect op name for NewWorkConn.

     > QUIC stream leak.

* ## [v0.46.0 [2022/12/18]](#v0.46.0[2022/12/18])
    * ### New
     > Add oidc_scope parameter to frpc when authentication_method = oidc.

     > Support quic protocol between frpc and frps.

    * ### Improve
     > Upgrade oidc and oauth2 package which is forward compatible.

* ## [v0.45.0 [2022/11/03]](#v0.45.0[2022/11/03])
    * ### Improve
     > Adjust http group load balancing to forward requests to each frpc proxy round robin. Previous behavior is always forwarding requests to a single proxy in the case of single concurrency.

* ## [v0.44.0 [2022/07/11]](#v0.44.0[2022/07/11])
    * ### New
     > Use auto generated certificates if plugin_key_path and plugin_crt_path are empty for plugin https2https and https2http.
    
     > Server dashboard supports TLS configs.

    * ### Fix
     > xtcp error with IPv6 address.

* ## [v0.43.0 [2022/05/28]](#v0.43.0[2022/05/28])
    * ### New
     > Added route_by_http_user in http and tcpmux proxy to support routing to different clients by HTTP basic auth user.
    
     > CONNECT method can be forwarded in http type proxy.
     
     > Added tcpmux_passthrough in tcpmux proxy. If true, CONNECT request will be forwarded to frpc.
 
* ## [v0.42.0 [2022/04/22]](#v0.42.0[2022/04/22])
    * ### New
     > Added new parameter config_dir in frpc to run multiple client instances in one process.
   
    * ### Fix 
     > Equal sign in environment variables causes parsing error.
 
* ## [v0.41.0 [2022/03/24]](#v0.41.0[2022/03/24])
    * ### New
     > Support go http pprof.

    * ### IMPROVE
     > Change underlying TCP connection keepalive interval to 2 hours.
     
     > Create new connection to server for sudp visitor when needed, to avoid frequent reconnections.

* ## [v0.40.0 [2022/03/13]](#v0.40.0[2022/03/13])
    * ### New
     > Added dial_server_timeout in frpc to specify connecting timeout to frps.

     > Additional EndpointParams can be set for OIDC.

     > Added CloseProxy operation in server plugin.

    * ### Improve
     > Added some randomness in reconnect delay.

    * ### Fix
     > TLS server name is ignored when tls_trusted_ca_file isn’t set.

* ## [v0.39.1 [2022/02/09]](#v0.39.1[2022/02/09])
    * ### Fix
     > Fixed IPv6 address parse issue.

* ## [v0.39.0 [2022/01/28]](#v0.39.0[2022/01/28])
    * ### New
     > Added connect_server_local_ip in frpc to specify local IP connected to frps.

     > Added tcp_mux_keepalive_interval both in frpc and frps to set tcp_mux keepalive interval seconds if tcp_mux is enabled. After using this params, you can set heartbeat_interval to -1 to disable application layer heartbeat to reduce traffic usage(Make sure frps is in the latest version).

    * ### Improve
     > Server Plugin: Added client_address in Login Operation.
     
    * ### Fix
     > Remove authentication for healthz api.
    
* ## [v0.38.0 [2021/10/28]](#v0.38.0[2021/10/28])
    * ### New
     > Add /healthz API.

     > frpc support disable_custom_tls_first_byte .If set true, frpc will not send custom header byte.

    * ### Improve
     > Use go standard embed package instead of statik.

* ## [v0.37.1 [2021/08/04]](#v0.37.1[2021/08/04])
    * ### Fix
     > Plugin https2https not work.

     > context canceled problem for http_proxy plugin when multiple requests reuse same connection.

     > In some cases, frps can't get server name for https proxy.

* ## [v0.37.0 [2021/06/03]](#v0.37.0[2021/06/03])
    * ### New
     > frpc add subcommand verify to validate configures before running.
     
     > frpc support includes option to split multiple proxy configs into different files.
     
     > Support sudp in dashboard.

    * ### Fix
     > Use empty string as default value for dashboard user and password.
     
     > login_fail_exit is not valid when protocol = kcp.
     
* ## [v0.36.2 [2021/03/22]](#v0.36.2[2021/03/22])
    * ### Improve
     > Support reverseproxy to dashboard with additional parts in path.

    * ### Fix
     > Fix logic error when parsing configs.

* ## [v0.36.1 [2021/03/19]](#v0.36.1[2021/03/19])
    * ### Fix
     > Fix bind_udp_port listen on error port.

* ## [v0.36.0 [2021/03/17]](#v0.36.0[2021/03/17])
    * ### New
     > New plugin https2https.

     > frpc supports tls_server_name to override the default value from server_addr.

    * ### Improvement
     > Increase reconnect frequency if it occurs an network error between frpc and frps

* ## [v0.35.1 [2021/01/25]](#v0.35.1[2021/01/25])
    * ### Fix
     > Reduce binary file size.

* ## Shell Upadte [2021/01/24]
    * ### Amend
     > Aliyun download url replace by Gitee download url

* ## [v0.35.0 [2021/01/20]](#v0.35.0[2021/01/20])
    * ### New
     > Server Plugin supports HTTPS.

    * ### Fix
     > Fix IPv6 address parse problem.

     > HTTP type proxy can't handle websocket protocol due to error Connection header value.

* ## [v0.34.3 [2020/11/20]](#v0.34.2[2020/11/20])
    * ### New
     > Command line parameters support enable_prometheus.

* ## [v0.34.2 [2020/11/12]](#v0.34.2[2020/11/12])
    * ### Fix
     > Stream data transfer delay(e.g. chunked data) for HTTP type proxy.

* ## [v0.34.1 [2020/10/01]](#v0.34.1[2020/10/01])
    * ### New
     > Support NTLM protocol for http proxy to connect frps.

     > Official docker image support on DockerHub and Github registry.

    * ### Fix
     > Fix a dashboard stats data lost problem after client reconnect more than 7 days.

     > Fix TLS certificate verification failed.


* ## [v0.34.0 [2020/09/19]](#v0.34.0[2020/09/19])
    * ### New
     > Support TLS certificate and mutual TLS authentication.

     > Support set max UDP package size, default is 1500.

     > New e2e test framework.

    * ### Fix
     > UDP and SUDP proxy don't support compression and encrytion.

     > Call server plugins in fixed order.

* ## [v0.33.0 [2020/04/27]](#v0.33.0[2020/04/27])
    * ### New
     > Server plugin add NewUserConn interface.

     > New proxy type sudp to provide a safe way to expose udp service like stcp.

     > Support load balancing for tcpmux.

    * ### Fix
     > Fix invalid of AuthenticateNewWorkConns in frpc.
      
     > Fix a panic problem if accept many connections concurrently.

* ## [v0.32.1 [2020/04/03]](#v0.32.1[2020/04/03])
    * ### NEW
     > New operation Ping and NewWorkConn support in Server Plugin.

     > Add apiVersion and op params in Server Plugin HTTP request.

    * ### Improvement
     > Prevent frequently relogin when connection broken after login success soon.

    * ### Fix
     > Fix a memory leak problem caused by frequently relogin.

* ## Shell Upadte [2020/03/24]
    * ### Add
     > Add new download url-gitee，just support install package

* ## [v0.32.0 [2020/03/11]](#v0.32.0[2020/03/11])
    * ### New
     > Support tls_only = true in frps.ini to enforce frps only accept TLS connection.
     
     > Set detailed_errors_to_client = false in frps.ini to hide detailed error information to client.  
     
     > Support prometheus monitor.
     
     > Optional OIDC authentication.  
     
     > New proxy type tcpmux. Support TCP port multiplexing over HTTP Connect tunnel.
    * ### Fix
     > Bandwidth limit configure not compared correctly when reloading.
     
     > Incorrect connection count stats.

* ## [v0.31.2 [2020/02/05]](#v0.31.2[2020/02/05])
    * ### Fix
     > Fix not release port when client start proxy error.
     
* ## [v0.31.1 [2020/01/06]](#v0.31.1[2020/01/06])
    * ### Fix
     > Fix panic when proxy meta data is set.

* ## [v0.31.0 [2020/01/03]](#v0.31.0[2020/01/03])
    * ### New
     > New server manage plugin to extend frp's ability
    * ### Improvement
     > Improve xtcp's success rate in some special case.

* ## [v0.30.0 [2019/11/29]](#v0.30.0[2019/11/29])
    * ### New
     > Support bandwidth limit for each proxy.
     
     > New plugin https2http, explore https service as http protocol.

* ## [v0.29.1 [2019/11/03]](#v0.29.1[2019/11/03])
    * ### Fix
     > Fix bug when use_encryption is true for xtcp.

* ## [v0.29.0 [2019/08/30]](#v0.29.0[2019/08/30])
    * ### New
     > New disable_log_color configure to disable console log color.
     
     > Plugin https2http support attatch headers by plugin_header_ prefix.
    * ### Change
     > Provide a high-level Go API.
    * ### Fix
     > max_pool_count is invalid.
     
     > Judge error between IPv4 and IPv6 in proxy protocol

* ## [v0.28.2 [2019/08/10]](#v0.28.2[2019/08/10])
    * ### Fix
     > Fix a bug that health check worker may stop unexpected.

* ## [v0.28.1 [2019/08/08]](#v0.28.1[2019/08/08])
    * ### New
     > Update standard http ReverseProxy to handle more upgrade protocol
     
     > Update some vendor packages.

* ## [v0.28.0 [2019/08/03]](#v0.28.0[2019/08/03])
    * ### New
     > type http support load balancing.
    * ### Fix
     > Fix a connection leak problem when login_fail_exit is false.

* ## [v0.27.1 [2019/07/15]](#v0.27.1[2019/07/15])
    * ### Fix
     > Add read timeout for TLS connection check.

* ## [v0.27.0 [2019/04/25]](#v0.27.0[2019/04/25])
    * ### New
     > Proxy Protocol support plugin unix_domain_socket.
     
     > frps support custom 404 page.

* ## [v0.26.0 [2019/04/10]](#v0.26.0[2019/04/10])
    * ### New
     > Support Proxy Protocol.
     
     > New plugin https2http.
    * ### Fix
     > Fix router config conflict when frpc start by command line mode. #1165

* ## [v0.25.3 [2019/03/26]](#v0.25.3[2019/03/26])
    * ### Fix
     > Fix panic error when reconnection with tls_enable is true.

* ## [v0.25.2 [2019/03/25]](#v0.25.2[2019/03/25])
    * ### Change
     > Change Update version of kcp-go.
    * ### Fix
     > Fix connection leak of http health check. #1155

* ## [v0.25.1 [2019/03/15]](#v0.25.1[2019/03/15])
    * ### Fix
     >Fix a match problem with multilevel subdomain. #1132  
      frps --log_file is useless. #1125

* ## [v0.25.0 [2019/03/11]](#v0.25.0[2019/03/11])
    * ### New
     > Support TLS between frpc and frps, Set
 tls enable to enable this feature in frpC.Improve stability of xtcp.
    * ### Fix
     > Fix a bug that xtcp don't release connections in some case.
     
    ##### Note: xtcp is incompatible with old versions.
 
    ##### 注意:此版本的xtcp和之前版本不兼容,需要同步升级服务端和客户端才能正常使用
 
* ## [v0.24.1 [2019/02/12]](#v0.24.1[2019/02/12])
    * ### Fix
     > Fix Error clear frpc configure file when /api/config called without token set
     
* ## [v0.24.0 [2019/02/11]](#v0.24.0[2019/02/11])
    * ### New
     > New Support admin UI for frpc
     
* ## [v0.23.3 [2019/01/30]](#v0.23.3[2019/01/30])
    * ### Fix
     > Fix Reload proxy not saved after reconnecting
  
* ## [v0.23.2 [2019/01/26]](#v0.23.2[2019/01/26])  
    * ### Fix 
     > Fix client not working caused by reconnecting.

* ## [v0.23.1 [2019/01/16]](#v0.23.1[2019/01/16])  
    * ### Fix 
     >Fix status api.
     
     >Fix reload and status command error.

* ## [v0.23.0 [2019/01/15]](#v0.23.0[2019/01/15])
    * ### New
     >Support render configure file template with os environment.
    * ### Change
     >Remove check for authentication timeout.
