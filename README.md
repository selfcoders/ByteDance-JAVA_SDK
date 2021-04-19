# -ByteDance-JAVA_SDK-
自写字节跳动JAVA_SDK包
近期因为工作需要对接字节跳动的小程序,调用官方接口的时候发现没有提供SDK就自写了一份SDK代码,有需要者自提,有疑问或者代码有问题可以留言或者添加Q:873302708,接口都是都是调测过没问题的;

以下是项目中用到的依赖：

```
<dependencies>
        <!-- https://mvnrepository.com/artifact/com.alibaba/fastjson -->
        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>fastjson</artifactId>
            <version>1.2.73</version>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <version>1.18.18</version>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-log4j2</artifactId>
            <version>2.1.9.RELEASE</version>
        </dependency>
    </dependencies> 
```
```
Maven导入命令: mvn install:install-file -Dfile=service.sdk-1.0.jar -DgroupId=com.selfcode.bytedance.service.sdk  -DartifactId=service.sdk -Dversion=1.0 -Dpackaging=jar
```
```
        public static void main(Stirng[] args){
                // dev:是否为开发环境,url:请求地址域名,根据入参更改
                // 默认情况下url参数可传"",为空的情况下使用默认域名
                // dev参数目前为true和false无区别,因为字节跳动没有提供测试环境和正式环境域名地址
                ServiceActuator serviceActuator = new ServiceActuator(true,"");
                // 创建对应的请求实体类对象封装入参,PS:目前暂不考虑优化实体类字段问题
                Code2Session code2Session = new Code2Session();
                // 将参数set入字段即可
                code2Session.setAnoymous_code("匿名code");
                code2Session.setCode("code");
                code2Session.setAppid("appid");
                code2Session.setSecret("秘钥");
                // 返回参数使用JSONObject封装方便读取
                JSONObject result = serviceActuator.code2Session(code2Session,0,0);
                // =============内容安全检测接口Demo====================
                ContentSafe contentSafe = new ContentSafe();
                // 创建内部类用以封装入参,多个数据的情况下创建多个对象进行封装
                ContentSafe.Content content = new ContentSafe.Content();
                content.setContent();
                contentSafe.setTasks(Arrays.asList(content));
                HashMap<String,Object> headers = new HashMap<String,Object>();
                // 请求头参数自定义传入,PS:暂不优化
                headers.put("X-Token","X-Token数据");
                // 复用请求执行器,可以考虑将请求执行器放入Spring的容器中进行复用
                result = serviceActuator.contentSafe(contentSafe,headers,0,0);
        }
        
```
