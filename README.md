# DidiLogistics

## [安卓端](https://github.com/87803/DidiLogistics) [服务器端](https://github.com/87803/DidiLogistics-serve)

## 本系统是一个滴滴物流的模拟系统：

1. 编写 Android 客户端应用，具有货主、货车司机注册、登陆以及需求信息发布功能。
2. 用 JSP 或 PHP 开发“滴滴物流”Web 服务器。
3. 用 MySQL 做“滴滴物流”Web 服务器的后台数据库。
4. 服务器端货主、货车司机供需匹配功能。
5. 客户端供需匹配成功与否显示功能。
6. 在线支付功能。

## 本系统安卓端使用MVVM + View Model + Data binding，服务器端使用Servlet+Tomcat，数据库使用MySQL、Redis，客户端和服务器端通过HTTP请求json数据。

### 以下是本系统实现的主要功能：

#### --登录注册功能：

1. 登录使用手机号 + 密码
2. 注册时可选择用户角色为货主或者司机
3. 密码使用MD5加密
4. 用户登录后，会在本地保存用户信息，下次打开应用时，会自动登录
5. 用户登录后，服务器会返回一个token，用于后续的请求，未经认证的请求会被拒绝
6. 注册时，会发送验证码到用户手机，用户输入验证码后才能注册成功
7. 登录后，自动根据用户角色跳转到货主或者司机的主界面

#### --货主端功能：

1. 发布需求，起点可使用高德api获取当前位置，系统会计算距离和推荐最低价格，用户输入价格不得低于推荐价格
2. 需求页可查看自己的所有需求
3. 司机页可查看处于接单状态且符合自己需求的司机，可向司机推送自己的需求
4. 司机页可根据司机位置筛选司机
5. 消息页可查看自己的所有消息，点击后可查看对应订单详情
6. 个人页可查看自己的个人信息，可修改个人信息，退出登录
7. 所有页面均可刷新数据
8. 订单详情页可查看订单的详细信息，订单处于待接单或已接单时可取消订单，可支付订单
9. 支付订单时，会调用支付宝支付，支付宝使用沙箱版，支付成功后，订单状态会变为已支付
10. 订单在接单之前，可与司机商议最终价格，货主在此期间可修改订单价格，接单后，价格不可修改

#### --司机端功能：

1. 需求页显示货主发布的需求，只显示司机货车能够满足的需求
2. 需求页可根据位置筛选需求
3. 司机可以查看需求的详细信息，进行接单、开启行程、完成订单等操作
4. 订单页可查看自己的所有订单，点击后可查看对应订单详情
5. 消息页可查看自己的所有消息，点击后可查看对应订单详情
6. 个人主页可查看自己的个人信息，累计收入，可修改个人信息，退出登录
7. 个人信息页可修改接单/不接单状态，可修改车辆信息

#### --服务器端功能：

1. 数据的增删改查
2. 认证过滤器，登录成功后返回token，后续请求只有携带合法的token才能获取到数据
3. 邮箱验证码发送功能（代替手机验证码api）
4. 验证码使用redis缓存，有效期为5分钟
5. 订单的相关操作只能由用户本人进行操作
6. mysql每日运行定时任务，将过期的订单进行取消操作
7. 司机未接单时，查看订单详情，会隐去详细地址，保证货主的隐私

#### 一些屏幕截图

屏幕截图为早期版本，部分功能以实际为准

1. 货主
   ![货主1](app/src/ScreenShot/user1.jpg)

2. 货主
   ![货主2](app/src/ScreenShot/user2.jpg)

3. 司机1
   ![司机](app/src/ScreenShot/driver1.jpg)

4. 司机2
   ![司机](app/src/ScreenShot/driver2.jpg)

5. 司机3
   ![司机](app/src/ScreenShot/driver3.jpg)