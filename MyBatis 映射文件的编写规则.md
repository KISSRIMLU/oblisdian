
```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
  PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
  "http://mybatis.org/dtd/mybatis-3-mapper.dtd">

<mapper namespace="com.sky.mapper.EmployeeMapper">
    <!-- 必须和 Mapper 接口的包路径+接口名一致 -->    
    <select id="getById" resultType="com.sky.entity.Employee">
    <!--id 必须和接口方法名一致-->
    <!--查询语句必须写resultType-->
    <!-- 参数占位符用 #{}防止注入-->
        select * from employee where id = #{id}
    </select>
</mapper>

```