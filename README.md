# webchat
用tornado+jQuery实现WebSocket聊天室

# 部署说明：
  1. 调试模式
     1.1 自动加载
         通过向Application实例传入参数debug=True，可以将程序以调试模式启动。比如：
         def make_app():
             return tornado.web.Application([
                # 路由
                ],
                debug = True
              )
         在这种模式下可以实现入戏便利。
          ＊ 自动加载：对项目中任何＊.py源文件修改将导致程序自动重启并加载修改后对代码文件。
          ＊ 错误追溯：当requestHandler处理用户访问出现异常时，系统的错误信息调用栈将被推送到浏览器中。
          ＊ 禁用模版缓存：在运营环境中模版缓存能提高效率，但在调试期间占用了更多当系统资源，所以将其禁用有利于开发者进行调试。
          
     1.2 运营期配置
         虽然tornado的内置IOLoop服务器可以直接作为运营服务器运行，但部署一个应用到生产环境面临着最大化利用系统资源的新挑战。因为Tornado的异步特            性，无法用大多数Python的网络框架标准WSGI进行站点部署，为了强化Tornado的应用请求吞吐量，在运营环境中通常采用反向代理＋多 Tornado后台实例          部署策略。通过Internet DNS服务器将用户浏览器的访问定位到多台nginx服务器上，每台nginx服务器又将访问重定向到多台Tornado服务端上。多个              Tornado服务既可以部署在一台服务器上，也可以部署在多台物理机上。
