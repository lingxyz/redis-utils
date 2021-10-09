# redis-utils
redis快捷方法和配置封装

### 使用
```java
/* controller */
@RestController
public class SpringBootController {
  // 注入
  @Autowired
  private RedisUtils redisUtils;
  @RequestMapping(...)
  public String hello(@PathVariable(value="id") String id) {
    // 查询缓存中是否存在
    boolean hasKey = redisUtils.exists(id);
    // 获取缓存
    Object object = redisUtils.get(id);
    // 写入缓存
    redisUtils.set(id, "xxx", 10L, TimeUnit.MINUTES);
  } 
}
```

```java
/* domain */
@Component
@EnableCaching
@CacheConfig(cacheNames = "user")
public class UserDomain {
  // 注入
  @Autowired
  private UserDao dao;

  @Cacheable(value="id=", key="#id")
  public User findById(String id) {
    return dao.findById(id);
  } 
}
```

### 技术选型
- Java 11
- Gradle
