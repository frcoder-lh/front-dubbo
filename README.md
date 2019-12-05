# front-dubbo
前后端调用框架


## 背景
dubbo框架解决了java程序之间远程调用的问题，我们还需要一个框架解决前后端调用的问题。
最简单的设想就是通过java controller层的代码生成js api层的代码。


## 设计
+ 后端程序通过`***/front-dubbo/api.js`接口，生成js的api层代码。
+ 前端程序通过引入`***/front-dubbo/api.js`作为js文件，就可以直接使用了。


## 特点
1. 一次引入，无需修改（不需要随着后端接口的修改而调整api层）
2. api层的代码结构与controller层保持一致


## 使用

### 1. 引入jar包

#### Maven

```xml
<dependency>
    <groupId>com.frcoder</groupId>
    <artifactId>front-dubbo</artifactId>
    <version>0.0.0</version>
</dependency>
```

#### Gradle

``` groovy
compile 'com.frcoder:front-dubbo:0.0.0'
```

### 2. 正常编写后端代码
```java
@Validated
@Path("/frcoder")
@Api(description = "活动相关接口")
@Produces({MediaType.APPLICATION_JSON})
@Consumes({MediaType.APPLICATION_JSON, MediaType.APPLICATION_FORM_URLENCODED})
public interface ActivityServiceApi {

    @GET
    @Path("/v1/activity")
    @ApiOperation(value = "获取活动信息", httpMethod = "GET", response = Response.class, tags = {"活动"})
    @ApiResponses(value = {
            @ApiResponse(code = 200, message = "code=0:SUCCESS99:其它错误", response = ActivityDto.class),
            @ApiResponse(code = 400, message = "参数错误"),
            @ApiResponse(code = 500, message = "服务内部错误")})
    Response<ActivityDto> getActivity(
            @ApiParam(value = "活动id", required = true) @NotNull @QueryParam("id") Long Id
    );
}
```

### 3. 前端引入js文件

```html
<script src="***/front-dubbo/api.js"></script>
```

### 4. 前端通过api层代码直接调用后端程序
```js
// 获取id为1的活动信息
var activity = $api.ActivityServiceApi.getActivity(1);
```
