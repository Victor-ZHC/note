# spring-boot

1. Spring Boot
* Application类：@SpringBootApplication
* Main方法：SpringApplication.run(Application.class, args);
* @Autowired自动导入依赖的bean

2. Spring Web MVC框架
* @Controller负责业务控制，与页面交互，就是struts中的action
* @Service负责业务逻辑，就是service或manager
* @Repository持久层，就是dao
* @Component，就是组件，确定不了哪一层使用

3. Controller中注解
* @RequestMapping返回值通常解析为跳转路径，将方法映射到HTTP请求
* 加上@ResponseBody，则不解析为路径
* @PathVariable路径变量，如：/{id}
```
RequestMapping(“user/get/mac/{id}”) 
public String getByMacAddress(@PathVariable int id){ } 
```
* @RequestParam方法参数
```
public void deleteApi(@RequestParam("id") int id){ }
```
* 关于@RestController
    * @RestController = @ResponseBody + @Controller
    * 一般想返回string或者json则用@RestController，想页面跳转则用@Controller

4. Service中注解
* @Transactional(readOnly = true)
    * @Transactional规定接口、类或者方法必须应用事务的元数据语法

5. JPA注解
* @Entity @Table：表明这是一个实体类，一般一起使用，如果表名和实体类名相同，则@Table可省略
* @Colum：如果字段名与列名相同，可省略
* @Id：主键
* application.properties中设置属性值