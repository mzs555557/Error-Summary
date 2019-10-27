#### Spring端口的设置及页面路由的设置

```
application.properties

server.port = 8088 //更改启动端口为8088
server.servlet.context-path = /test //规定启动路由


```

#### Spring的路由设置

```
@Component
@ConfigurationProperties(prefix = "boot")
public class ConfigInfo {
    private String name;
    private String location;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getLocation() {
        return location;
    }

    public void setLocation(String location) {
        this.location = location;
    }
}




@Controller
public class ConfiginfoController {
    
    @Autowired
    private ConfigInfo configInfo;

    @RequestMapping("/boot/config")
    public @ResponseBody String config() {

        return configInfo.getLocation() + "   " + configInfo.getName();
    }
}


--------第二种方法
----application.properties
#自定义配置
boot.name = test1
boot.localtion = test2

-----

@Controller
public class ConfiginfoController {
    @Value("${boot.name}")
    private String name;

    @Value("${boot.location}")
    private String location;

    

    @RequestMapping("/boot/config")
    public @ResponseBody String config() {

        return name + "-----" + location;
    }
}
```

#### MVCController

```
@RestController
public class MVCController {
    @RequestMapping("/boot/getUser")
    public Object getUser() {
        User user  = new User();
        user.setId("100");
        user.setName("马总帅");
        return  user;
    }
    @RequestMapping(value = "/boot/getUser1" , method = RequestMethod.GET)
    public Object getUser1(){
        User user = new User();
        user.setId("120");
        user.setName("马总帅2");
        return user;
    }
    @GetMapping("/boot/getUser2")
    public Object getUser2(){
        User user = new User();
        user.setId("140");
        user.setName("this ");
        return user;

    }
}

```

#### jsp在Spring中的配置

```

```
