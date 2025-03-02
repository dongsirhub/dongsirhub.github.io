# 3、简述 SpringMVC 中如何返回 JSON 数据

**Step1：**在项目中加入json 转换的依赖，例如jackson，fastjson，gson 等

**Step2****：**在请求处理方法中将返回值改为具体返回的数据的类型，例如数据的集合类

List<Employee>等

**Step3：**在请求处理方法上使用@ResponseBody 注解



> 更新: 2024-05-01 15:28:13  
> [原文](https://www.yuque.com/zhichangzhishiku/edrbqg/itp0wlkgwqkdmd9w>