# 1、简单的谈一下 SpringMVC 的工作流程

● 用户发送请求至前端控制器DispatcherServlet

● DispatcherServlet 收到请求调用HandlerMapping 处理器映射器。

● 处理器映射器找到具体的处理器，生成处理器对象及处理器拦截器(如果有则生成)一并返回给DispatcherServlet。

● DispatcherServlet 调用HandlerAdapter 处理器适配器

● HandlerAdapter 经过适配调用具体的处理器(Controller，也叫后端控制器)。

● Controller 执行完成返回ModelAndView

● HandlerAdapter 将controller 执行结果ModelAndView 返回给

DispatcherServlet

● DispatcherServlet 将ModelAndView 传给ViewReslover 视图解析器

● ViewReslover 解析后返回具体View

● DispatcherServlet 根据View 进行渲染视图（即将模型数据填充至视图中）。

DispatcherServlet 响应用户



> 更新: 2024-05-03 22:58:21  
> [原文](https://www.yuque.com/zhichangzhishiku/edrbqg/zrd6gtlocbth9o15>