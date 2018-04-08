# play-mall
play mall shop


# Play Mall 电商平台功能

## 前台功能

## 商家中心

## 管理员功能

# 平台架构

# APP架构
## 技术选型

## 接口设计

## 数据层设计

## 业务层设计

## 呈现层设计


# 多平台认证设计
## 账号密码
## 客户端会话Token
功能：充当Session的角色，不同的客户端有不同的生命周期。

步骤：
    1.用户使用账号密码，换取会话Token
    
Web平台生存周期短，移动端生存周期长
## Access_Token
功能：服务端应用程序API接口访问和调用的凭证

使用：
    1.使用具有较长生命周期的会话Token获取此接口访问Token

## pam_Token(PC Auth Mobile)
功能：由已经登录和认证的PC端生成的二维码的原始串号（Pc Auth Mobile）。

步骤：
    1. PC上用户已经完成认证，登录了系统
    2. PC端生成一组和此用户相关联的pam_token
    3. PC端将此pam_token的使用链接生成二维码
    4. 移动端扫码后，请求服务器，并和用户信息关联
    5. 移动端获取refresh_token(长时效的会话)
    6.根据 refresh_token 获取 access_token
    7.完成正常的接口调用工作
    
备注:
1.生存周期为2分钟,2分钟后过期删除
2.没有被使用时,每1分钟变一次
3.被使用后,立刻删除掉
4.此种认证模式一般不会被使用到
## map_Token(Mobile Auth PC)
功能：由已经登录的移动app来扫码认证PC端系统，并完成PC端系统的登录（Mobile Auth Pc）。

主要步骤：

1.移动端完成用户身份的认证登录app
2.未登录的PC生成匿名的 map_token
3.移动端扫码后在db中生成 map_token 和用户关联（完成签名）
4.db同时针对此用户生成 web_token
5.PC端一直以 map_token 为参数查找此命名用户的 web_token
6.PC端根据 web_token 去获取 access_token
7.后续正常的调用接口调用工作

备注:

1.生存周期为2分钟,2分钟后过期删除
2.没有被使用时,每1分钟变一次
3.被使用后,立刻删除掉