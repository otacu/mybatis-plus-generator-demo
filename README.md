### mybatis plus 代码生成
这里只是代码生成，实际项目中还可以使用mybatis plus的其它特性。

默认模板在mybatis-plus-generator包的templates目录下，可以拷贝出来修改，然后用代码指定自定义的模板。

例如我加了自动填充@TableField(fill = FieldFill.INSERT)之后，还要在实际项目那里实现个填充器
````
import com.baomidou.mybatisplus.core.handlers.MetaObjectHandler;
import org.apache.ibatis.reflection.MetaObject;
import org.springframework.stereotype.Component;

import java.util.Date;

/**
 * 在entity加了FillFeild注解之后，还要实现这个填充器
 */
@Component
public class MybatisObjectHandler implements MetaObjectHandler {
    @Override
    public void insertFill(MetaObject metaObject) {
        setFieldValByName("createTime", new Date(),metaObject);
        setFieldValByName("updateTime",new Date(),metaObject);
    }
    @Override
    public void updateFill(MetaObject metaObject) {
        setFieldValByName("updateTime",new Date(),metaObject);
    }
}
````