# 编写规范
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
# 标签语句
#### 1. `<if>` - 条件判断
```xml
<!-- 最简单的条件拼接 -->
<select id="list" resultType="Employee">
    select * from employee
    where 1=1
    <if test="name != null and name != ''">
        and name like concat('%', #{name}, '%')
    </if>
    <if test="status != null">
        and status = #{status}
    </if>
</select>
```
#### 2. `<where>` - 智能处理 WHERE
```xml
<!-- 自动处理多余的 AND/OR，如果没有条件就不生成 WHERE -->
<select id="list" resultType="Employee">
    select * from employee
    <where>
        <if test="name != null">
            and name = #{name}  <!-- 第一个条件前的 and 会被自动去掉 -->
        </if>
        <if test="status != null">
            and status = #{status}
        </if>
    </where>
</select>

```
#### 3. `<set>` - 智能处理 SET（用于 update）
```xml
<!-- 自动处理多余的逗号 -->
<update id="update">
    update employee
    <set>
        <if test="name != null">name = #{name},</if>
        <if test="status != null">status = #{status},</if>
        <if test="age != null">age = #{age},</if>
    </set>
    where id = #{id}
</update>
```