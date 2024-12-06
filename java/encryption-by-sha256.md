# Encryption by SHA-256
> Java provides `MessageDigest` class.  
> Use such methods as `getInstance(String algorithm)`, `update(byte[] input)` and `digest()` for SHA-256 encryption.  
> 
> You must be aware that MessageDigest class is not thread-safe! Use a new instance of it for every single thread.

```java
import java.security.MessageDigest;
import java.security.NoSuchAlgorithmException;

public class SHA {
  
  public String encryptBySha256(String text) throws NoSuchAlgorithmException {
    MessageDigest md = MessageDigest.getInstance("SHA-256");
    md.update(text.getBytes());
    
    return bytesToHex(md.digest());
  }
  
  private String bytesToHex(byte[] bytes) {
    StringBuilder builder = new StringBuilder();
    for (byte b : bytes) {
      builder.append(String.format("%02x", b));
    }
    return builder.toString();
  }

}
```
