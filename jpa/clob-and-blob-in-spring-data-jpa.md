# CLOB and BLOB in Spring Data JPA

> In Spring data JPA, fields are converted to DBMS columns in such ways as the below.  
> * String, char[] and java.sql.CLOB => CLOB  
> * byte[], java.sql.BLOB => BLOB  


```java
@Table(name = "LOB_TEST")
@Entity
@AllArgsConstructor(access = AccessLevel.PROTECTED)
@NoArgsConstructor(access = AccessLevel.PROTECTED)
@Builder
@Getter
public class LobTestEntity {
  
  @Id
  @GeneratedValue(strategy = GenerationType.IDENTITY)
  @Column(name = "ID", nullable = false)
  private Long id;

  @Lob
  @Column(name = "LOB_TEXT", length = 65535, nullable = false)
//  @Column(name = "LOB_TEXT", columnDefinition = "TEXT")
  private String lobText;
}
```

## Use the annotation `@LOB`
Put @LOB on fields that you'd like for CLOB or BLOB.

## Set `length` property in the annotation `@column` in range of the Type you would like.
Without this setting, if Mariadb, the string gets to be converted to `TINYTEXT` as the property's default value is 255.  
So, when you set the length property with a number in range of `TEXT`, which is from 256 to 65535, the field is to be converted to TEXT.  
`MEDIUMTEXT` and `LONGTEXT` can be made in the same way.

## @LOB is better than `@Column(columnDefinition = “TEXT”)` in terms of portability.
You can also make TEXT field with "columnDefinition" property.  
But, if it is possible to change DBMS, this could be challenging to change all lines to get rid of the property settings as, for example, ORACLE has no TEXT type.  
If you use @LOB, Oracle DBMS creates CLOB for the field.  
