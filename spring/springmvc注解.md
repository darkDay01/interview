# springmvc注解

1.@RestController

相当于控制层类上@Controller和方法@ResponseBody同时加上，也就是Restful风格的请求处理方式，该控制类内的所有方法返回的均是json对象格式。

2.@GetMapping (查询)

相当于方法上@RequestMapping（value="XXX", method=RequestMethod.GET）

**3.@PostMapping（新增）**

相当于方法上@RequestMapping（value="XXX", method=RequestMethod.POST）

4.@DeleteMapping（删除）

相当于方法上@RequestMapping（value="XXX", method=RequestMethod.DELETE）

5.@PutMapping（更新）

相当于方法上@RequestMapping（value="XXX", method=RequestMethod.PUT）

6.@PathVariable

获取URL中的参数数据

# Restful风格



![image-20210418172502403](C:\Users\文文\AppData\Roaming\Typora\typora-user-images\image-20210418172502403.png)

![image-20210418172539716](C:\Users\文文\AppData\Roaming\Typora\typora-user-images\image-20210418172539716.png)

如果同样的请求方式和url：

![image-20210418173246423](C:\Users\文文\AppData\Roaming\Typora\typora-user-images\image-20210418173246423.png)

java.lang.IllegalStateException: **Ambiguous handler methods mapped for** '/user/detail/1/wenwen': {public java.lang.Object com.fanqie.controller.TestController.getUserInfos(java.lang.Integer,java.lang.String), public java.lang.Object com.fanqie.controller.TestController.getUserInfo(java.lang.Integer,java.lang.String)}...
请求路径冲突解决方式：

1.不同的请求注解：@GetMapping、@PostMapping、@DeleteMapping、@PutMapping

2.修改请求路径：/user/detail/{id}/{address} -->  /user/{id}/detail/{address}