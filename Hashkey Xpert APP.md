<font size=6 > **HashKey Xpert 产品需求文档** </font>

## 版本变更记录

| 序号 | 变更内容                                                     | 变更人 | 变更时间   |
| ---- | ------------------------------------------------------------ | ------ | ---------- |
| 1    | 新增Sprint1.0.0:   1、登录注册、忘记密码、修改密码、绑定/修改手机、修改邮箱 | 黄金叶 | 2022-03-14 |

<!-- TOC -->

    - [版本变更记录](#版本变更记录)
- [1.全局说明](#1-全局说明)
- [2.登录注册](#2-登录注册)
    - [2.1 注册](#21-注册)
    - [2.2 登录](#22-登录)
    - [2.3 忘记密码](#23忘记密码)
    - [2.4 登出](#24登出)
- [3. 用户中心](#3-用户中心)
    - [3.1 安全设置](#31安全设置)

<!-- /TOC -->

# 1.全局说明

**切面切换保护：**

* 当程序切换到后台时，在预览状态下，所有页面要模糊保护处理
    * 仅对IOS系统。
    * 安卓需要禁止截屏抓取页面才可实现，目前APP需要支持截屏，所以暂不实现。

**全局错误提示样式及类型：**

UI设计稿待补充

| 编号 | 场景               | 提示类型  | 消息类型  | Duration |
| ---- | ------------------ | --------- | --------- | -------- |
| 1    | Toast01（操作后）  | Toast01   | Success   | 2s       |
| 2    | 错误提示（操作后） | Toast02   | Error     | 2s       |
| 3    | 警告信息（操作后） | Toast03   | Alert     | 2s       |
| 4    | 短提示信息         | Toast04   | info      | 2s       |
| 5    | 长提示信息         | Toast05   | info      | 2s       |
| 6    | 按钮加载           | loading01 | loading01 |          |
| 7    | 列表加载           | loading02 | loading02 |          |
| 8    | 列表加载           | loading03 | loading03 |          |
| 9    | 页面加载           | loading04 | loading04 |          |

**弹窗类型：**

| 编号 | 场景                                   | 提示类型 | 消息类型         | Duration |
| ---- | -------------------------------------- | -------- | ---------------- | -------- |
| 1    | 二次确认（确认）                       | Modal01  | Confirm          | -        |
| 2    | 二次确认（确认/取消）                  | Modal02  | Confirm/Cancel   | -        |
| 3    | 二次确认（操作1//操作2/取消）          | Modal03  | 操作1/操作2/取消 | -        |
| 4    | 带标题二次确认（操作1/操作2/取消）     | Modal04  | 操作1/操作2/取消 | -        |
| 5    | 带标题图标二次确认（操作1/操作2/取消） | Modal05  | 操作1/操作2/取消 | -        |
| 6    | 输入框校验 （输入框下方出现提示）      | input01  | -                | -        |

* 网络加载失败
    * 提示类型：toast04
    * 中文提示语：网络加载失败,请重试
    * 英文提示语：Failed to load,retry.
* 加载数据超时
    * 提示类型：toast04
    * 中文提示语：加载数据超时
    * 英文提示语：Loading timeout
* 内部服务器程序运行错误时
    * 提示类型：toast04
    * 中文提示语：服务暂时不可用哟，请稍后再试   
    * 英文提示语：Service is temporarily unavailable, please retry later   



**区域码（按照英文或拼音的A-Z排序）：**

* 国家/地区列表待补充
* 国家/地区下拉列表统一从后端获取配置文件（除Jumio身份信息校验国家地区从Jumio后端获取）
  * 注册登录页面，注册手机号下拉选项
  * 提示类型：Toast04 
    校验规则：提交的为受限地区（不支持的国家） 
    文提示语：根据最新监管政策要求，目前暂不支持向受限地区用户提供服务  
    英文提示语：In response to the latest regulatory policy requirements, the restricted territory is temporarily suspended.  

**手机系统功能**

* 【IOS】支持手机自动读取短信填入输入框

  

**相关域名链接：**

* 用户协议：待补充
* 隐私政策：待补充
* APP下载链接：待补充

**短信发送限制**

* 单个号码为每分钟一条，到达限制后，需提示“You have sent too many requests,Please try again later"

* 单个号码每天限制40条，到达限制后，需提示“Daily limit reached”

   

# 2.登录注册

## 2.1 注册

### 2.1.1 功能概述

为实现Hashkey用户在一次注册后能够使用HashKey各业务线的产品和服务，提升用户体验、优化开发资源，需要将Xpert、Hub、Bcts进行账户整合，打造全新的APP

### 2.1.2 业务流程

注册流程：

1. 进入注册页面
2. 填写手机或邮箱 
3. 校验帐户(邮箱、手机号)为空校验、人机验证、唯一性、格式校验
4. 人机验证
5. 调用第三方发送验证码
6. 填写验证码，验证注册账号
7. 验证码为空校验、时效性校验、正确校验
8. 设置密码
9. 密码为空校验、格式校验、复杂度校验
10. 注册成功
11. 绑定Google认证
12. 自动登录，进入首页

### 2.1.3 UI设计稿

原型链接：[https://modao.cc/app/iXralQe8r7qyr5vnldcmkw 《Xpert》](https://modao.cc/app/iXralQe8r7qyr5vnldcmkw 《Xpert》) 

UI链接：https://lanhuapp.com/web/#/item/project/stage?tid=e44db160-5031-4fb1-a111-760af024f228&pid=58a1b682-293a-4980-a789-9dc5b2e16749

### 2.1.4 需求详述

**前置条件**

* 通过页面点击或者跳转进入注册页面

**交互逻辑**

* 【创建账户//Create account】
    * 手机或邮箱填写完成后，点击”下一步//Next“，进入人机验证页面；需校验填写的手机或邮箱是否注册成功，若已注册成功，需提示“手机号码已存在//Phone number already exists"，“邮箱已存在//Email already exists”
    * 点击“登录//Login in”，进入到登录页面
    * 点击“User Agreement, Privacy Policy ”，进入协议查看页面，点击“关闭”按钮，关闭当前页面
* 人机校验通过后，进入【手机/邮箱认证//Verify phone/Email】页面，验证成功后，点击”下一步Next“，进入【设置密码//Create a password】页面
* 【设置密码//Create a password】，设置成功后，点击“确认//Confim"，进入【谷歌认证//Google Authentication】页面
* 【谷歌认证Google Authentication】，验证成功后，点击“确认//Confim"，进入到【Login】页面

**页面元素**

【创建账户//Create account】 

* 用户名默认为用户注册账号，手机号或邮箱

* 选择区域码（不支持输入）：默认填充中国香港的区号（+852）。
    * 根据IP填入区域码
    * 点击区域码，底部出现弹窗显示
    * 国家/地区//Country/Region
    * 点击“取消//Cancel”，关闭当前弹窗
    * 确认//OK，填入选择
    
* 对应区域码参看概述“区域码”章节。
    * 排序规则：中文按照拼音a-z排序，英文按照字母a-z排序。
    
* 手机//Phone：默认显示“请输入您的手机号//Enter phone number”，限制最多输入11位数字字符长度。

    * 提示类型：Input01    
    场景：手机号为空         
    备注：不可进行下一步  

    * 提示类型：Toast01    
      场景：校验手机号格式，仅为数字         
      中文提示语：手机号格式错误      
      英文提示语：Invaild phone number    

* 邮箱//Email：默认提示“请输入您的邮箱//Enter email”，限制最多输入50个字符。

    * 提示类型：Toast01  
    场景：邮箱格式不正确 
    校验原则：以“@”符号及“.xx”作为格式校验依据       
    中文提示语：邮箱格式不正确    
    英文提示语：Invalid Email address  
    备注：失焦校验  
    * 提示类型：Input01   
      场景：邮箱输入为空      
      备注：不可进行下一步   

【人机校验】

* 安全验证//Account Security
  * 人机安全验证//Anti-Bot Detection

【手机/邮箱认证//Verify phone/Email】

* 脱敏的手机（含区号）或邮箱
* 短信验证码，默认提示：短信验证码//SMS code
* 邮箱验证码，默认提示：邮箱验证码//Email code
* 黏贴//Paste，点击后填入表单
   * 非数字6位，则提示（Toast04）“不符合格式要求//Invalid format”
   * 为空则提示（Toast04）“剪贴板没有内容//Clipboard is blank”
* 按钮“发送验证码//Send”，用户点击“发送验证码//Send”按钮在发送成功后将显示为“60s”，可再点击“重新发送//Resend。
* 输入6位后，正确校验通过，自动进入下一个页面
* 发送至邮箱，显示脱敏邮箱
* 手机时标题显示“验证手机//Verify Phone”，邮箱时标题显示“验证邮箱//Verify Email”

* 手机号或邮箱，点击“下一步"按钮，弹出滑动人机验证 ，验证成功后，发送验证码。 

    * 提示类型：Toast04  
    校验规则：发送验证码24小时超过发送限制（IP/手机号）    
    中文提示语：发送已达当日上限   
    英文提示语：Daily limit reached

    * 提示类型：Toast04  
      校验规则：发送验证码频率，24小时最多发送40次    
      中文提示语：邮箱验证码发送次数已达上限    
      英文提示语：Email verification has reached the upper limit

    * 提示类型：由人机验证控件决定      
      校验规则：由人机验证进行操作判断  
      备注1：默认首先开启无感验证，发现有风险后，才升级验证方式（比如滑块等）    


         中文          |             英文             
        ---------------------- | ---------------------------- 
        拖动下方的滑块         | Drag the slider below        
        加载失败，请重试       | Loading error, please retry  
        加载中...              | Loading...                   
        无感验证成功           | Success                           
        请向右拖动滑块完成验证 | Drag the slider to the right 
        智能检测中             | Detecting                    
        验证成功               | Success                      
        验证失败               | Verify Error    
        验证失败，请重试        | Verify Error, please retry               
        验证中                 | Verifying                    

* 

    * 提示类型：Toast04  

        校验规则：发送验证码24小时超过发送限制（IP/手机号）
        中文提示语：发送已达当日上限   
        英文提示语：Daily limit reached

    * 提示类型：Toast04  
        校验规则：发送验证码频率，24小时最多发送40次    
        中文提示语：邮箱验证码发送次数已达上限    
        英文提示语：Email verification has reached the upper limit

    * 提示类型：Toast_04    
      场景：区域码+手机号不合法，或发送短信功能异常  
      校验原则：发送短信功能异常  
      中文提示语：发送短信失败，请重试  
      英文提示语：Send sms error, please retry     
      备注：点击人机验证通过后，产生的发送失败

    * 提示类型：Toast_04  
      场景：发送短信与上次短信成功发送的时间间隔未大于60秒  
      校验原则：再次发送短信与上次短信成功发送的时间需要大于60秒  
      中文提示语：发送间隔太短，请1分钟后再试         
      英文提示语：Frequent request detected, retry 1 min later     

    * 提示类型：Toast_04  
      场景：发送邮件与上次邮件成功发送的时间间隔未大于60秒  
      校验原则：再次发送邮件与上次邮件成功发送的时间需要大于60秒  
      中文提示语：发送间隔太短，请1分钟后再试         
      英文提示语：Frequent request detected, retry 1 min later   

    * 提示类型：Toast01    
      场景：验证短信发送成功    
      校验原则：电话区号与手机号码输入正确且验证短信发送成功  
      中文提示语：短信发送成功  
      英文提示语：Success   

    * 提示类型：Toast01    
      场景：验证邮箱发送成功    
      校验原则：邮箱输入正确且验证邮箱发送成功  
      中文提示语：邮件发送成功  
      英文提示语：Success    

    * 提示类型：Toast01    
      场景：人机验证失败    
      校验原则：获取的token与后端检验不一致  
      中文提示语：验证失败，请稍后再试  
      英文提示语：Authentication failed, please retry   

* 仅支持输入6位的验证码，自动校验，验证码状态：有效、失效、过期。校验与提示如下：

    * 提示类型：Toast_04    
      场景：未点击发送按钮获取验证码       
      校验原则：未点击发送按钮获取验证码    
      中文提示语：请发送验证码     
      英文提示语：Please send code        

    * 提示类型：Toast01   
    场景：验证码输入校验错误  
    校验原则：验证码正确性    
    中文提示语：验证码错误  
    英文提示语：Incorrect code      
    备注：容许2次错误，第3次需要重新发送

    * 提示类型：Toast04  
    场景：存在填写的验证码格式不正确    
    校验原则：验证码只能为6位整数    
    中文提示语：不符合格式要求   
    英文提示语：Invalid format     
    备注：点击“确认登录” 提交验证   
    
    * 提示类型：Toast01   
	场景：验证码输入校验错误2次，第3次做失效处理  
	校验原则：验证码正确性和有效性，且为6位整数，    
	中文提示语：验证码错误多次，请重发  
    英文提示语：Incorrect code, please get a new one     
	备注：验证码做失效处理。

    * 提示类型：Toast01   
    场景：验证码已输入6位数字，但验证码过期。或成功后得验证码失效处理。     
    校验原则：验证码不能过期  
    中文提示语：验证码过期，请重发    
    英文提示语：Code expired, please get a new one       
    备注：短信5分钟过期，邮件30分钟过期   

【设置密码//Create a password】

* 密码//Password
   * 输入框提示：请输入密码//Enter the password
   * 逻辑限制：输入限制长度8-30位字符
* 提示语：8-30位字符/8-30 characters   
   * 如新密码输入框有值，但输入不符合描述标准，显示红字

* 隐藏眼睛：支持密码的明文隐藏与显示切换，默认第一次输入默认隐藏。
* 黏贴//Paste，点击后填入剪贴板
   * 非数字或字母，则提示（Toast04）“不符合格式要求//Invalid format”
   * 为空则提示（Toast04）“剪贴板没有内容//Clipboard is blank”
* 按钮：确认//Confirm

* 点击确认，依次校验如下规则：

    *  场景：密码输入为空  
      校验原则：密码不能为空  
      备注：为空，按钮置灰显示 
* 完成注册：所有验证通过，完成注册。
  * 提示类型：Toast01    
    场景：用户注册成功并进入谷歌认证页面，默认登录状态 
    校验原则：用户注册成功并进入谷歌认证页面 ，默认登录状态 
    中文提示语：注册成功   
    英文提示语：registered successfully 

【谷歌认证//Google Authentication】

* 密钥二维码

* 具体密钥的明文显示

* 复制谷歌密钥//Copy Google Secret Key 

* 文案提示：

    * 复制谷歌密钥后，前往谷歌验证器中绑定//After copying Google Secret Key, go to Google Authenticator to bind.
    * 开启谷歌验证操作指引按钮：如何绑定并开启谷歌认证? 点击查看> //How to bind and activate GA? Click to check >
    * 如何开启谷歌认证，点击后页面打开H5的FAQ的相关文章页面，
        * 简体链接：待补充
        * 英文链接：待补充
        * 繁体链接：待补充

* 谷歌验证码//GA Code

    * 输入框提示：输入上方的谷歌验证码// Enter the above GA Code
    * 输入限制：限制只能输入6位数字

     * 按钮：粘贴//Paste：
       * 点击后黏贴复制的验证码，非数字6位，则提示（Toast04）“不符合格式要求//Invalid format”
       * 为空则提示（Toast04）“剪贴板没有内容//Clipboard is blank”

 * 按钮：确认//Confirm

    * 点击“确认//Confirm”按钮，如未填写谷歌验证码提示：

        * 提示类型：Toast04  
          场景：谷歌验证码为空  
          校验原则：谷歌验证码不能为空       
          中文提示语：请输入谷歌验证码   
           英文提示语：Enter the  Google Verification Code   
          备注：点击键盘内“确认”按钮   

         * 提示类型：Toast04  
           场景：存在填写的验证码格式不正确   
           校验原则：验证码只能为6位整数   
           中文提示语：不符合格式要求   
           英文提示语：Invalid format     
           备注：点击“确认//Confirm” 提交验证     
    * 绑定谷歌认证结果：

        * 场景1：成功绑定谷歌认证    
          提示类型：Toast01  
          中文提示语：谷歌认证成功     
          英文提示语：Activated      
          备注：成功跳转至首页

        * 场景2：谷歌认证失败    
          提示类型：Toast02    
          中文提示语：谷歌认证失败            
          英文提示语：Activation Failed       
          备注：停留在当前页面，并清除已输入验证码     

## 2.2 登录

###  2.2.1 功能概述

注册成功后的用户，可以正常登录Xpert APP，并可以访问对应的功能

### 2.2.2 业务流程

登录流程：

1. 填写手机号或邮箱
2. 填写密码
3. 帐户和密码的为空校验、格式校验、输错校验
4. 新设备校验
5. 输入手机验证码/谷歌验证码
6. 手机验证码/谷歌验证码为空校验、时效性校验、正确校验
7. 登录成功
8. 绑定GA校验
9. 未绑定则进入【谷歌认证Google Authentication】，已绑定则进入首页

### 2.2.3 UI设计稿

原型链接：[https://modao.cc/app/iXralQe8r7qyr5vnldcmkw 《Xpert》](https://modao.cc/app/iXralQe8r7qyr5vnldcmkw 《Xpert》) 

UI链接：https://lanhuapp.com/web/#/item/project/stage?tid=e44db160-5031-4fb1-a111-760af024f228&pid=58a1b682-293a-4980-a789-9dc5b2e16749

### 2.2.4 需求详述

**前置条件**

* 用户已注册成功

**交互逻辑**

- 【登录//Log in】
  - 点击”登录//Log in“, 校验成功后，若是新设备，则进入到人机验证页面,人机认证通过后，进入到【验证//Verification】页面；若非新设备，则直接进入到【验证//Verification】页面
  - 点击”忘记密码//Forget password“，进入到【重设密码//Reset Password】页面
- 【验证//Verification】
  - 默认选中“Hashkey谷歌认证//Hashkey/Google Auth”，点击”提交//Submit“，校验成功后，登录成功，进入到首页
  - 可切换选中”手机认证//Phone Verification",点击”发送//Send",发送验证码，显示倒数60s，结束后，按钮变为“重新发送//Resend"；点击”提交//Submit“，校验成功后，登录成功
  - 判断用户是否已绑定GA，若未绑定，则弹窗强制要求进行绑定；若已绑定，则直接进入首页

**页面元素**

【登录//Log in】

* 选择区域码（不支持输入）：默认填充中国香港的区号（+852）。
  * 根据IP填入区域码
  * 点击区域码，底部出现弹窗显示
  * 国家/地区//Country/Region
  * 点击“取消//Cancel”，关闭当前弹窗
  * 确认//OK，填入选择

* 对应区域码参看概述“区域码”章节。
  * 排序规则：中文按照拼音a-z排序，英文按照字母a-z排序。

* 手机//Phone：默认显示“请输入您的手机号//Enter phone number”，限制最多输入11位数字字符长度。

  * 提示类型：Input01    
    场景：手机号为空         
    备注：不可进行下一步  

  * 提示类型：Toast01    
    场景：校验手机号格式，仅为数字         
    中文提示语：手机号格式错误      
    英文提示语：Invaild phone number    

* 邮箱//Email：默认提示“请输入您的邮箱//Enter email”，限制最多输入50个字符。

  * 提示类型：Toast01  
    场景：邮箱格式不正确 
    校验原则：以“@”符号及“.xx”作为格式校验依据       
    中文提示语：邮箱格式不正确    
    英文提示语：Invalid Email address  
    备注：失焦校验  
  * 提示类型：Input01   
    场景：邮箱输入为空      
    备注：不可进行下一步  

 * 登录密码//Login Password：限制最大可输入长度30个字符，默认提示“请输入密码//Enter the password”密码输入默认隐藏(点击后，图标点亮，明文显示)。校验规则如下，如校验不通过，进行提示。

    * 提示类型：Input01  
	场景：密码输入为空  
	校验原则：密码不能为空     
	备注：为空不可进入下一步

	* 提示类型：Input01  
	场景：密码不符合规范  
	校验原则：8-30位，不能为空  
	中文提示语：8-30位字符    
    英文提示语：8-30 characters  
	备注：失焦或点击登录按钮校验    
* 登录：账号密码输入为空，登录按钮灰化无法点击。点击“登录”后，除上述校验规则与提示外，其他校验及提示方式如下。

    * 提示类型：Toast01    
	场景：用户登录成功  
	校验原则：所有验证正确     
	备注：登录校验通过后，进入到2FA认证页面 
    * 提示类型：Toast01  
	  场景：账号密码不匹配  
	  校验原则：账号不存在，或账号与密码不匹配  
      中文提示语：帐号或密码不正确   
	  英文提示语：User name or Password is  incorrect 
	* 提示类型：Toast_04  
	  场景：登录超时,登录态保持3天  
      校验原则：登录时间超过3天  
	  中文提示语：登录超时  
      英文提示语：Login session expired  
	  备注：以每次输入帐户和密码的登录后开始计算 

【验证//Verification】

* 谷歌认证//Hashkey/Google Auth
  * 文案展示：输入6位谷歌验证码//Enter the 6-digit code from Authenticator
  * 输入框对应文案：Hashkey谷歌验证码//Hashkey/Google verification code
* 手机认证//Phone Verification
  * 文案展示：输入发送至手机(掩码展示)的6位验证码//Enter the 6-digit code sent to 18***107
  * 输入框对应文案：手机验证码//Mobile verification code
  * 点击“发送//Send"，后端调用短信服务商发送验证码短信至用户绑定的手机号，显示倒数60s，结束后，按钮变为“重新发送//Resend”  

* 点击“提交//Submit"，仅支持数字输入，校验规则如下：
    * 提示类型：Toast01    
      场景：用户登录成功  
      校验原则：所有验证正确  
      中文提示语：登录成功   
      英文提示语：Logged in    
      备注：登录校验通过后，判定是否已绑定GA  
    * 若为新设备登录判断，如果发现用户是以往设备中的新设备（不包括第一次），则需要发送异常登陆邮件/短信提醒至用户对于邮箱和手机
    * 提示类型：Toast04  
    场景：存在未填写的验证码   
    校验原则：验证码不能为空    
    中文提示语：验证码不能为空    
    英文提示语：Code cannot be blank      
    备注：点击“提交//Submit" 提交验证  
    * 提示类型：Toast04  
    场景：存在填写的验证码格式不正确    
    校验原则：验证码只能为6位整数    
    中文提示语：不符合格式要求   
    英文提示语：Invalid format     
    备注：点击“提交//Submit"提交验证     
    * 提示类型：Toast04   
    场景：验证码输入校验错误  
    校验原则：验证码正确性    
    中文提示语：验证码错误  
    英文提示语：Incorrect code      
    备注：容许2次错误，3次输对机会，谷歌验证例外
    * 提示类型：Toast04   
      场景：验证码输入校验错误2次，第3次做失效处理  
      校验原则：验证码正确性和有效性，且为6位整数        
      中文提示语：验证码错误多次，请重发  
      英文提示语：Incorrect code, please get a new one     
      备注：验证码做失效处理。
    * 提示类型：Toast04   
      场景：验证码已输入6位数字，但验证码过期。或成功后得验证码失效处理。     
      校验原则：验证码不能过期  
      中文提示语：验证码过期，请重发    
      英文提示语：Code expired, please get a new one       
      备注：短信5分钟过期，邮件30分钟过期，谷歌按照谷歌过期时间
* 【绑定GA弹窗】
  * 标题：温馨提示//Tips
    正文：为给您提供持续稳定的服务，建议您绑定谷歌验证。//To provide you with better services, please bind Google Authentication to your account.
    按钮：立即绑定//Set Up
    点击，进入谷歌验证页面

**其他说明：**

* 异常IP登录，邮件或短信提醒，具体查看短信邮件模版。

  

## 2.3 忘记密码

### 2.3.1 功能概述

用户在忘记密码的情况下，需要提供重置密码功能

### 2.3.2 业务流程

忘记密码流程：

1. 点击“忘记密码”
2. 进入重置密码页面
3. 填写手机号或邮箱
4. 人机验证，调用第三方服务发送验证码
5. 填写验证码
6. 重新设置密码，并进行二次确认
7. 完成修改，进入登录页面，重新进行登录

### 2.3.3 UI设计稿

原型链接：[https://modao.cc/app/iXralQe8r7qyr5vnldcmkw 《Xpert》](https://modao.cc/app/iXralQe8r7qyr5vnldcmkw 《Xpert》) 

UI链接：https://lanhuapp.com/web/#/item/project/stage?tid=e44db160-5031-4fb1-a111-760af024f228&pid=58a1b682-293a-4980-a789-9dc5b2e16749

### 2.3.4 需求详述

**前置条件**

* 登录页面，点击“忘记密码”。

**交互逻辑**

* 【忘记密码//Forget password】
  * 点击”下一步//Next“，需校验填写的手机或邮箱需是否注册成功，若未注册成功，需提示“用户不存在//User no exists”,验证成功后，进行人机校验
* 人机校验通过后，进入【手机/邮箱认证//Verify phone/Email】页面，验证成功后，点击”下一步Next“，进入【重置密码//Reset password】页面
* 【重置密码//Reset password】，设置成功后，点击“确认//Confim"，进入到登录页面

**页面元素**

【忘记密码//Forget password】

* 文案展示：For security purpose,no withdrawals are allowed for 24 hours after security changes.
* 校验规则同注册模块2.1.4【创建账户//Create account】 ，不再复述

【手机/邮箱认证//Verify phone/Email】

* 同注册模块2.1.4【创建账户//Create account】 ，不再复述

【重置密码//Reset password】

* 新密码//New password
  * 请输入密码//Enter the password
* 确认密码//Confirm
  * 再次确认密码//Confirm the password
* 密码本身的校验规则:同“注册得密码设置”的校验，补充校验如下：
  * 提示类型：Toast04  
    场景：密码与确认密码不一致  
    校验原则：密码与第一次输入保持一致  
    中文提示语：请保持密码一致  
    英文提示语：Enter the same password    
    备注：点击“确定”按钮 
* 校验通过后，完成设置，进入登录页面。

## 2.4 登出

### 2.4.1 需求详述

**前置条件**

- 用户已成功登录

**交互逻辑**

- 用户进入【我的//Me】页面，点击“Log out",弹窗确认，确认后成功登出

**页面元素**

- 【确认登出弹窗】
  - 提示类型：Modal02
  - 提示语：确认要退出登录？//Are you sure you want to log out?
  - 确认//Confirm：进行登出，成功后到登录页面。
  - 关闭//Close：点击后，关闭当前弹窗。

# 3.用户中心

## 3.1 安全设置

### 3.1.1 功能概述

为保障用户账号安全，一期需实现用户登录密码修改、绑定邮箱、绑定/修改手机功能

### 3.1.2 UI设计稿

待补充

### 3.1.3 需求详述

【安全设置//Security Settings】

* 页面元素：
    * 标题：安全设置//Security Settings

       * 登录密码//Login Password
           * 修改//Edit

       * 谷歌认证//Google Authentication
           * 未设置//Disabled
           * 修改//Edit
       * 手机认证//Mobile Authentication
           * 未设置//Disabled
           * 修改//Edit
       * 邮件认证//Email Authentication
           * 未设置//Disabled
           * 邮箱设置后，不可修改，显示具体的用户绑定邮箱，
             * 显示逻辑：显示开始和最后4个字符，中间字符固定显示3个“*”
    * 点击左上角“返回//Back”，返回上一页。

#### 3.1.3.1 修改登录密码

**前置条件**

* 用户登录状态
* 点击安全设置的修改密码

**页面元素**

* 标题：修改密码//Change Password
* 展示文案：登录密码修改后，转账功能将被禁止24小时。//The transfer function will be disabled for 24 hours after Login Password has been changed.
* 旧密码//Original Password 
   * 输入框提示：请输入旧密码//Please enter the original password
   * 逻辑限制：限制最大可输入长度20个字符
* 新密码//New Password
   * 输入框提示：请输入新密码//Please enter the new password
   * 逻辑限制：限制最大可输入长度30个字符
* 密码提示语：8-30位字符//8-30 characters
   * 如新密码输入框有值，但输入不符合描述标准，显示红字

* 隐藏眼睛：密码全部密文显示，点击右侧“眼睛图标”(点击后，图标点亮）显示明文。

* 点击“确认//Confirm”，依次校验如下规则，如校验不通过，进行提示。

    * 提示类型：Toast04   
	场景：旧密码输入为空   
	校验原则：旧密码不能为空    
	中文提示语：请输入旧密码  
    英文提示语：Please enter the original password  
	备注：提交校验。 

    * 提示类型：Toast04 
	场景：新密码输入为空  
	校验原则：新密码不能为空  
	中文提示语：请输入新密码  
    英文提示语：Please enter the new password  
	备注：提交校验。 

    * 提示类型：Toast04 
	场景：新密码格式不符合要求   
	校验原则：8-30位字符   
	中文提示语：8-30位字符   
    英文提示语：8-20 characters  
	备注：提交校验。 
    
    * 提示类型：Toast04   
	场景：旧密码输错  
    校验原则：旧密码输错     
    中文提示语：原密码不正确      
    英文提示语：Password is incorrect   
	备注：提交校验。 

    * 提示类型：Toast04     
	场景：新密码与原密码相同  
    校验原则：新密码与历史所有设置过的原密码相同       
    中文提示语：新密码不能和旧密码相同       
    英文提示语：The new password can not be the same as the original one   
	备注：提交校验。 

* 校验通过后：

    * 场景1：成功修改密码  
    提示类型：Toast01  
    中文提示语：修改成功    
    英文提示语：Modified       
    备注：登出帐户，跳转登录页面重新登录  

    * 场景2：修改密码失败    
    提示类型：Toast02  
    中文提示语：修改失败     
    英文提示语：Modification Failed    
    备注： 保留之前的填写密码，页面不跳转     

**其他说明**

* 跳转登录页面重新登录，限制转账24小时。

#### 3.1.3.2 绑定/修改手机认证

**前置条件**

* 用户登录状态
* 点击安全中心的绑定手机认证

**页面元素**

* 标题：绑定手机//Bind Phone number 
  * 绑定手机时显示
* 标题：修改手机//Change Phone Number
  * 修改手机时显示
* 修改手机显示以下文案    
  * 手机号修改后，转账功能将被禁止24小时。//Transfer function will be disabled for 24 hours after phone number has been changed.
 * 手机//Phone
   * 输入框提示：请输入您的手机号//Enter your phone number
   * 限制最多输入11位数字字符长度。
 * 按钮：发送//Send
   * 点击发送后显示（60秒内）：60s
   * 点击发送后显示（大于60秒）：重新发送//Resend
         * 点击重新发送后显示（60秒内）：重新发送//Resend
         * 点击重新发送后显示（大于60秒）：重新发送//Resend
 * 验证码//Verification Code
   * 输入框提示：短信验证码//SMS Verification Code
   * 输入限制：限制只能输入6位数字
 * 粘贴//Paste 
   * 点击后黏贴复制的验证码，非数字6位，则提示（Toast04）“不符合格式要求//Invalid format”，为空则提示（Toast04）“剪贴板没有内容//Clipboard is blank”。

 * 确认//Confirm


* 点击绑定/修改手机页面“确认”,根据校验结果有如下提示：

  * 提示类型：Toast04  
    场景：手机号为空    
    校验原则：手机号不能为空       
    中文提示语：请输入您的手机号   
     英文提示语：Phone number cannot be blank   
    备注：点击键盘内“确认”按钮

  * 提示类型：Toast04  
    场景：验证码为空    
    校验原则：验证码不能为空      
    中文提示语：请输入验证码   
     英文提示语：Verification code cannot be blank   
    备注：点击键盘内“确认”按钮

   * 提示类型：Toast04  
     场景：存在填写的验证码格式不正确   
     校验原则：验证码只能为6位整数   
     中文提示语：不符合格式要求    
     英文提示语：Invalid format     
     备注：点击“确认//Confirm” 提交验证  

* 点击绑定/修改手机页面“确认”,校验通过，进入安全认证页面（旧手机验证）：
  * 手机显示开始2个字符，最后3个字符，中间部分数字固定显示4个“*”
  * 交叉认证时，SMS下方的提示语（仅限于修改SMS认证的交叉安全认证）
    * 交叉验证标题：安全认证//Security Authentication
    * 旧的短信认证一旦丢失，请联系客服//Once original SMS Authentication is lost, please contact our customer service.

* 安全认证校验通过后：

  * 场景1：成功绑定手机认证    
    提示类型：Toast01    
    中文提示语：手机认证成功          
    英文提示语：Verified       
    备注：成功跳转安全中心     

  * 场景2：绑定手机认证失败      
    提示类型：Toast02     
    中文提示语：手机认证失败         
    英文提示语：Verification Failed           
    备注：停留在当前页面   

**其他说明**

* 手机验证绑定成功，跳转至安全设置页面，手机认证显示”编辑//Edit",可修改
* 修改手机认证，发邮件或短信提醒用户，限制转账24小时

#### 3.1.3.1 绑定邮箱认证

**前置条件**

* 用户登录状态
* 点击安全中心的绑定邮箱认证

**页面元素**

* 标题：绑定邮箱//Bind Email
* 提示文案1:开启后邮箱不能更改//Unable to change when mailbox was activated.
* 提示文案2:如果没有收到邮件，请查看邮箱的垃圾箱//If you haven't received Email, please check the trash mailbox.
* 邮箱//Email
   * 输入框提示：请输入您的邮箱//Enter your email
   * 逻辑限制：限制最多输入100个字符。
* 按钮：发送//Send
    * 点击发送后显示（60秒内）：60s
    * 点击发送后显示（大于60秒）：重新发送//Resend
           * 点击重新发送后显示（60秒内）：重新发送//Resend
               * 点击重新发送后显示（大于60秒）：重新发送//Resend
* 验证码//Verification Code
   * 输入框提示：邮箱验证码//Email Verification Code
   * 输入限制：限制只能输入6位数字

* 按钮：粘贴//Paste 
    * 点击后黏贴复制的验证码，非数字6位，则提示（Toast04）“不符合格式要求//Invalid format”，为空则提示（Toast04）“剪贴板没有内容//Clipboard is blank”。

* 点击“确认”后，依次校验如下规则：
   * 提示类型：Toast04  
	场景：邮箱为空  
	校验原则：邮箱不能为空    
	中文提示语：请输入您的邮箱
    英文提示语：Please enter your email
	备注：点击键盘内“确认”按钮  

    * 提示类型：Toast04  
    场景：未填写的验证码 
       校验原则：验证码不能为空
       中文提示语：验证码不能为空  
       英文提示语：Verification cannot be blank.   
       备注：点击“确认//Confirm” 提交验证    
   
    * 提示类型：Toast04  
    场景：存在填写的验证码格式不正确
       校验原则：验证码只能为6位整数
       中文提示语：不符合格式要求
       英文提示语：Invalid format   
       备注：点击“确认//Confirm” 提交验证    


    英文提示语：Please fill in the correct email address
    备注：点击键盘内“确认”按钮  
    
    * 提示类型：Toast04  
    场景：邮箱格式不正确 
    校验原则：以“@”符号及“.xx”作为格式校验依据       
    中文提示语：邮箱格式不正确    
    英文提示语：Invalid Email address  
    备注：点击“确认//Confirm” 提交验证   
    
    * 场景1：成功绑定邮箱认证  
    提示类型：Toast01  
    中文提示语：邮箱认证成功     
    英文提示语：Verified.  
    备注：成功跳转安全中心    
    
    * 场景2：绑定邮箱认证失败    
    提示类型：Toast02  
    中文提示语：邮箱认证失败       
    英文提示语：Verification Failed     
    备注：停留在当前页面   

**其他说明**

* 成功绑定邮箱验证，跳转至安全设置页面，邮箱认证掩码显示已绑定好的邮箱，不可再点击

