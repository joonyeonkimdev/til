# How to Configure ObjectMapper
> Such methods of ObjectMapper class as `configure()`, `enable()` and `disable()`  have been deprecated since 2.13.  
> 
> Use `JsonMapper.builder()`!

```java
import com.fasterxml.jackson.databind.DeserializationFeature;
import com.fasterxml.jackson.databind.MapperFeature;
import com.fasterxml.jackson.databind.ObjectMapper;
import com.fasterxml.jackson.databind.json.JsonMapper;

public class ObjectMapperTest {
  
  public static void main(String[] args) {
    final ObjectMapper objectMapper1 = JsonMapper.builder()
            .configure(MapperFeature.ACCEPT_CASE_INSENSITIVE_PROPERTIES, true)
            .configure(DeserializationFeature.FAIL_ON_UNKNOWN_PROPERTIES, false)
            .build();
    
    final ObjectMapper objectMapper2 = JsonMapper.builder()
            .enable(MapperFeature.ACCEPT_CASE_INSENSITIVE_PROPERTIES)
            .disable(DeserializationFeature.FAIL_ON_UNKNOWN_PROPERTIES)
            .build();
  }
  
}
```
Those two ObjectMapper instances have the same configuration.
