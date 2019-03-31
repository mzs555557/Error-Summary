####模型封装的方法
```
public class Test extends ActionSupport implements ModelDriven<User> {
	private User user = new User();
	public User getModel() {
		return user;	
	}
}
```