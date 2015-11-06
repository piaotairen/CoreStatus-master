
    Charlin出框架的目标：简单、易用、实用、高度封装、绝对解耦！

# CoreStatus
   网络状态监听者：可监听2G/3G/4G ！
<br />
<br /><br />
框架截图   CUT
===============
![image](./CoreStatus/show.gif)<br />

<br /><br /><br />

组织信息 ORG
===============
成都iOS开发群：<br />
二群：369870753（新开，新鲜着呢，快加） <br />
一群：163865401（已爆满，加不上了）  <br /><br />
<br /><br /><br />


####注意：默认程序没有反应，你需要在真机手动改变网络环境才能看到效果！！！

<br /><br />

框架特性： FEATURE
===============
>1.基于苹果的Reachability封装。<br />
>2.对常用网络状态封装了简单API。<br />
>3.作为解耦的重要目的，本框架是其他很多重要Core框架的核心成员。<br />
>4.新增对2G、3G、4G网络检测支持。<br />
>5.增加实时检测，并屏蔽了注册通知及细节，直接使用即可，简单方便！<br />

<br /><br /><br />

使用说明 USAGE
===============
#### 1.导入框架

        #import "CoreStatus.h"

<br/><br/>
#### 2. 获取网络当前状态: 当前状态，非实时

        CoreNetWorkStatus currentStatus = [CoreStatus currentNetWorkStatus];
        
请注意当前状态是枚举，具体值如下：

        /** 网络状态 */
        typedef enum{
            
            /** 无网络 */
            CoreNetWorkStatusNone=0,
            
            /** Wifi网络 */
            CoreNetWorkStatusWifi,
            
            /** 蜂窝网络 */
            CoreNetWorkStatusWWAN,
            
            /** 2G网络 */
            CoreNetWorkStatus2G,
            
            /** 3G网络 */
            CoreNetWorkStatus3G,
            
            /** 4G网络 */
            CoreNetWorkStatus4G,
            
            /** 未知网络 */
            CoreNetWorkStatusUnkhow
        
        }CoreNetWorkStatus;

<br/><br/>
#### 3.当前状态中文说明文字：

    NSString * statusString = [CoreStatus currentNetWorkStatusString];


<br/><br/>
#### 4.实时监控：注册监听

    //调用一个方法即可
    [CoreStatus beginNotiNetwork:self];

请注意这个方法需要一个遵循了CoreStatusProtocol协议的对象，一般控制器遵循此协议：
然后请实现以下协议方法（optional）：

        -(void)coreNetworkChangeNoti:(NSNotification *)noti;
    



        注意：当网络改变，此协议方法会自行触发，我传了通知数据给你，示例有打印通知内容。
        当然，最简单的获取当前实时状态的方法是使用上面的静态状态获取，即：
        
        -(void)coreNetworkChangeNoti:(NSNotification *)noti{
            //因为这些是实时，所以每次的静态状态就是当前实时状态，你也可以从noti中取
            CoreNetWorkStatus currentStatus = [CoreStatus currentNetWorkStatus];
        }

<br/><br/>

#### 5.实时监控：移除监听
请特别注意：因为内部封装，所以你看不到监听过程，实际内部已经注册了通知。请注意用完需要关闭监听。
比如控制器不可见需要关闭监听：

    -(void)viewDidDisappear:(BOOL)animated{
        
        [super viewDidDisappear:animated];
        
        [CoreStatus endNotiNetwork:self];
    }

<br/><br/>
#### 6. 新增API：

        /** 是否是Wifi */
        +(BOOL)isWifiEnable;
        
        /** 是否有网络 */
        +(BOOL)isNetworkEnable;
        
        /** 是否处于高速网络环境：3G、4G、Wifi */
        +(BOOL)isHighSpeedNetwork;

<br/><br/>

致谢 THANKS
===============
感谢一号群成都iOS开发_Charlin（163865401，群已满）朋友深夜测试！！！感谢！

<br/><br/>
结束语 END
===============
其实有很多方法可以完成同样的事情，思路其实都是一样的。赶快投入组织的怀抱吧！
<br/><br/>

开源许可 License
===============
Charlin Feng的框架基于MIT license.您可点击License文件查看详情。
<br/><br/>
