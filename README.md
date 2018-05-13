# 设计模式

[TOC]



## 简单工厂模式

假设根据登录入口的不同，调用不同的处理方法

- QQ		QQLoginService
- wechat     WeChatLoginService
- github       GitHubLoginService

> 定义通用接口

```java
interface LoginService {
    /**
     * 登录平台
     * @return
     */
    boolean login();
}
```

> QQ登录实现

```java
public class QQLoginService implements LoginService {
    @Override
    public boolean login() {
        System.out.println("QQ do login");
        return true;
    }
}
```

> weChat登录实现

```java
public class WeChatLoginService implements LoginService {
    @Override
    public boolean login() {
        System.out.println("wechat do login");
        return true;
    }
}
```

> github登录实现

```java
public class GitHubLoginService implements LoginService{
    @Override
    public boolean login() {
        System.out.println("github do login");
        return true;
    }
}
```

> 简单工厂

```java
/**
 * 简单工厂
 *
 */
public class SimpleFactory {

    public LoginService createLogin(String platform){

        if("QQ".equals(platform)){
            return new QQLoginService();
        }else if("WeChat".equals(platform)){
            return new WeChatLoginService();
        }else if("GitHub".equals(platform)){
            return new GitHubLoginService();
        }

        return null;
    }
}
```

> 测试以及输出结果

```java
/**
 * 测试入口
 */
public class MainTest {
    public static void main(String[] args) {
        //QQ
        LoginService qqLogin  = new SimpleFactory().createLogin("QQ");
        qqLogin.login();

        //WeChat
        LoginService weChatLogin  = new SimpleFactory().createLogin("WeChat");
        weChatLogin.login();

        //GitHub
        LoginService githubLogin  = new SimpleFactory().createLogin("GitHub");
        githubLogin.login();
    }
}
```

```
QQ do login
wechat do login
github do login
```

[^总结]: 新增登录平台就需要修改工厂类，违反开闭原则

------

## 工厂方法模式

假设根据登录入口的不同，调用不同的处理方法

- QQ		QQLoginService
- wechat     WeChatLoginService
- github       GitHubLoginService

> 定义通用接口

```java
interface LoginService {
    /**
     * 登录平台
     * @return
     */
    boolean login();
}
```

> QQ登录实现

```java
public class QQLoginService implements LoginService {
    @Override
    public boolean login() {
        System.out.println("QQ do login");
        return true;
    }
}
```

> weChat登录实现

```java
public class WeChatLoginService implements LoginService {
    @Override
    public boolean login() {
        System.out.println("wechat do login");
        return true;
    }
}
```

> github登录实现

```java
public class GitHubLoginService implements LoginService{
    @Override
    public boolean login() {
        System.out.println("github do login");
        return true;
    }
}
```

> 工厂接口

```java
/**
 * 工厂接口(也可以用抽象类)
 */
public interface Factory {
    LoginService createLogin();
}
```

> QQ工厂实现类

```java
/**
 * QQ工厂具体类
 */
public class FactoryQQ implements Factory {
    @Override
    public LoginService createLogin() {
        return new QQLoginService();
    }
}
```

> wechat工厂实现类

```java
/**
 * wechat工厂具体类
 */
public class FactoryWeChat implements Factory {
    @Override
    public LoginService createLogin() {
        return new WeChatLoginService();
    }
}
```

> GitHub工厂实现类

```java
/**
 * github工厂具体类
 */
public class FactoryGitHub implements Factory{
    @Override
    public LoginService createLogin() {
        return new GitHubLoginService();
    }
}
```

> 测试以及输出

```java
/**
 * 测试入口
 */
public class MainTest {
    public static void main(String[] args) {
        //GitHub
        Factory factoryGit = new FactoryGitHub();
        LoginService gitHubLogin = factoryGit.createLogin();
        gitHubLogin.login();

        //QQ
        Factory factoryQQ = new FactoryQQ();
        LoginService loginQQ = factoryQQ.createLogin();
        loginQQ.login();

        //weChat
        Factory factoryWeChat = new FactoryWeChat();
        LoginService loginWeChat = factoryWeChat.createLogin();
        loginWeChat.login();
    }
}
```

```
github do login
QQ do login
wechat do login
```

[^优点]: 可扩展，不违反开闭原则
[^缺点]: emmm  类多多

------

## 抽象工厂模式

