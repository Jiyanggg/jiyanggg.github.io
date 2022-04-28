
## 为什么要使用 Enum 枚举类

枚举类是定义预设的常量，避免传入无效值引起异常， 可以使得代码更有可读性和健壮性。

## 使用 == 比较枚举类

避免值相同的两个不同的枚举类的比较, 出现不符合逻辑的情况

## EnumSet And EnumMap

可以使用 enumSet 和 enumMap 进行枚举类的一些操作 (配合  Stream API 可以简洁的进行包含, 取子集, 分组等操作)

### Enum & JSON

使用 FastJson 的注解可以增强枚举类的特性

### 例子

```java
public enum PinType {

    REGISTER(100000, "注册使用"),
    FORGET_PASSWORD(100001, "忘记密码使用"),
    UPDATE_PHONE_NUMBER(100002, "更新手机号码使用");

    private final int code;
    private final String message;

    PinType(int code, String message) {
        this.code = code;
        this.message = message;
    }

    public int getCode() {
        return code;
    }

    public String getMessage() {
        return message;
    }

    @Override
    public String toString() {
        return "PinType{" +
                "code=" + code +
                ", message='" + message + '\'' +
                '}';
    }
}
```

POJO 对象中有 Enum 类时的序列化和反序列的处理

```

@Data
class Qsm {
    String name;

    @JSONField(serialize = false, deserialize = false)
    MyEnum myEnum;

    @JSONField(name = "status")
    public String getState() {
        return Optional.ofNullable(myEnum).map(MyEnum::getCode).orElse(null);
    }

    @JSONField(name = "status")
    public void setState(String code) {
        this.myEnum = MyEnum.getEnumByCode(code);
    }
}

// 被引用
@Getter
@AllArgsConstructor
enum MyEnum {
    USAGE701("123", "正在营业");
    private String code;
    private String desc;

    private static final Map<String, MyEnum> CODE_MAP = new HashMap<>();

    static {
        for (MyEnum typeEnum : MyEnum.values()) {
            CODE_MAP.put(typeEnum.getCode(), typeEnum);
        }
    }

    public static MyEnum getEnumByCode(String code) {
        return CODE_MAP.get(code);
    }
}
```


### 其他

 序列化&反序列化 Enum 类: 
 
 https://my.oschina.net/yehun/blog/3047638
 
 https://www.cnblogs.com/insaneXs/p/9515803.html
 
 https://blog.csdn.net/u013541707/article/details/108393338


Baeldung 博文: https://www.baeldung.com/a-guide-to-java-enums