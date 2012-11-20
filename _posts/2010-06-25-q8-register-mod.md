---
layout: post
title: Q8实用注册表更改
date: 2010-06-25 15:07
comments: true
categories: []
---

今天又把机子刷了，列举一下可能用到的注册表更改

1. 个性化修改网标,把中国移动换成你需要的文字就可以了
[HKEY_LOCAL_MACHINESoftwareMicrosoftRILOperatorNames]
"46002"="中国移动"
"46001"="中国联通"
"46000"="中国移动"
2. [HKEY_CURRENT_USERSoftwareMicrosoftInboxSettingsOEM]
"SMSInboxThreadingDisabled"=dword:0       ;对话模式短信0启用，1关闭
3. [HKEY_CURRENT_USERSoftwareMicrosoftWindowsCurrentVersionExplorerShell Folders]
"Cache"="Storage CardPocket IETemporary Internet Files"
"Cookies" = "Storage CardPocket IECookies"
"History" = "Storage CardPocket IEHistory"    ;把IE的缓存文件 历史记录和Cookie存到SD卡上。刷机或者硬启不会丢失
4. [HKEY_LOCAL_MACHINEnlsoverrides]
"SSDte"="dddd yyyy-M-d" ;在Chome上显示星期几
5. 修改注册表提高系统速度
第1：HKEY_LOCAL_MACHINE/System/StorageManager/FATFS查看值/EnableCache：将原值1改为 3。
修改注册表以提高机器运行速度：
修改注册表 HKEY_LOCAL_MACHINESystemStoragManagerFATFSEnableCache
将原值1改成3，3为推荐数值，理论上越高越快，我修改为6，未发现问题，速度级大提升！
一些改善性能的修改（主要是该缓存，根据ROM版本不同，有些键可能在注册表中找不到，新建即可）
HKEY_LOCAL_MACHINESystemStorageManagerFATFSCacheSize=8192
HKEY_LOCAL_MACHINESystemStorageManagerFATFSEnableCache=1
HKEY_LOCAL_MACHINESystemStorageManagerFiltersfsreplxfiltReplStoreCacheSize=8192
HKEY_LOCAL_MACHINESystemStorageManagerProfilesMSFlashFATFSFiltersDataCacheSize=8192
HKEY_LOCAL_MACHINESystemStorageManagerProfilesMSFlashFATFSFlags=40
第2：HKEY_CURRENT_USER/ControlPanel/WIFI/里面的EapolParam1和EapolParam2这两项里面分别 有2个双字节值，将其四项全部改为256。
第3：HKEY_LOCAL_MACHINE/Security/WAP查看值/NetworkCount：将双字节值0改为128
另：修改注册表提高系统显示加速
[HKEY_LOCAL_MACHINESYSTEMGDIGLYPHCACHE]底下“limit”的值（正常是61440）改大即可。改到 92160，效果十分明显。不建议再大了，加大到（120000）以上也没发现问题！！！胆小的改到（76800）也行！原理为加大系统显卡的预读内存， 可以极好的优化效果！！！
6. 去掉初次运行程序时的安全警告：
HKEY_LOCAL_MACHINESecurityPoliciesPolicies000101a
= 1时不显示警告信息；
＝0时恢复显示。
7. 修改注册表延长待机时间
(1).[HKEY_LOCAL_MACHINECommAsyncMac1Parms]
"DisablePowerManagement"=dword:1
修改为："DisablePowerManagement"=dword:0
(2).[HKEY_LOCAL_MACHINECommIrsir1Parms]
"DisablePowerManagement"=dword:1
修改为："DisablePowerManagement"=dword:0
(3).[HKEY_LOCAL_MACHINECommPPTP1Parms]
"DisablePowerManagement"=dword:1
修改为："DisablePowerManagement"=dword:0
(4).[HKEY_LOCAL_MACHINECommL2TP1Parms]
"DisablePowerManagement"=dword:1
修改为："DisablePowerManagement"=dword:0
8. 去掉快门声音
[HKEY_LOCAL_MACHINEsystempicturescameraoemsoundfile]
修改soundfile的键值，将windowsshuttersound_02_secs.wav随便将 shuttersound_02_secs.wav去除一个字母即可
9. Q8照相全屏方法
(1)、打开HKEY-CURRENT-USER/software/microsoft/pictures/camera/user下的 fullscreen键值修改为1
(2)、打开HKEY-LOCAL-MACHINE/software/microsoft/pictures /camera/oem/ 找到HideFullScreenMenu键,键值修改为0,（作用是显示隐藏的全屏菜单）找到FitWindow键，键值修改为1（其作用是使全屏模式 下取景框充满整个屏幕）
(3)、如果感觉相机自动进入待机状态时间太短，修改StandBySec修改为你想要的时间，我改为25，这样25秒空闲后才弹出待机提示。
10. 屏蔽“短信已发送”的提示：
修注册表KEY_LOCAL_MACHINE/SOFTWARE/Microsoft/Inbox/SettingsSMSNoSentMsg”的将 Dword值从0改为1，软启便可。
11. 加快上网速度
HKEY_LOCAL_MACHINECommTcpIpParms处的TcpMaxConnetctRetransmissions键值十进制为 10，十六进制为A就可以了
12. CAB格式安装文件安装了以后避免被系统自动删除的俩个方法：
HKEY_LOCAL_MACHINESoftwareappsMicrosoft Application InstallernDynamicDelete
= 0 不自动删除；
= 2 默认自动删除
HKEY_CLASSES_ROOTcabfileShellopencommand
=wceload.exe "%1" /nodelete 不自动删除；
=wceload.exe "%1" 默认自动删除
13. 优化输入法的速度
[注册表：hkey_current_user/controlpanel/accessibility/
修改这两个字串 chartimeout 和 holdtimeout
chartimeout值是英文输入法的待选时间（就是按键后出现所按键的首字母并且下面有横线，这时可以多次按键选择次字母、第三字母的时 间）；holdtimeout是中文输入时选定汉字需要长按键的时间。
chartimeout通常400－500就可以了，再快就手忙脚乱了，holdtimeout建议200－300，甚至可以更低
要改回去缺省值是10000和800。
14. 短信铃声可以用wma、mp3等
打开注册表，找到HKEY_CURRENT_USER/ControlPanel/Sounds/SMS/....打开 “category”，将 “value data“ 的数值从 ”Notification“ 改为 "Ring" ；然后还要将
“HKEY_CURRENT_USER/ControlPanel/SoundCategories/Notification/” 里的 “Script”值拷贝到“HKEY_CURRENT_USER/ControlPanel/SoundCategories/Ring/”下即可
15. 修改开始菜单和桌面快捷方式顺序的方法？
以前一直想把qq和msn还有日程表等我不太常用的放到后面去,把常用的放到前面来.大家发现在StoragewindowsStart Menu里自己后来添或装进去的快捷方式是可以移动和改名的,SP原先带的都不能动没有移动删除修改的权限.其实菜单的顺序是可以修改注册表解决的.
菜单的第一页的顺序是固定的,从第2也开始是按字母顺序排的,英文前中文后,先快捷方式后文件夹.现在找 到"HKEY_CURRENT_USERSOFWAREMicrosoftShellStartmenu",然后修改其中的"Order",里 面会看到"Inbox.lnk Contacts.link......"这些就是原先SP默认的强制顺序,每个*.link都代表StoragewindowsStart Menu里面的一个快捷方式,删掉里面任何一个就可以看到他没有特权了也按字母顺序排了....
你只要把你想要的快捷方式加进来就可以了,格式要和其他一样独占一行,而且要注意大小写不能错.(当然要先看Storagewindows Start Menu里你需要的软件快捷方式叫什么名字).里面默认的有8个,自己添加可以加到8个以上的.只是8个以后从第2页开始算起的.关于文件夹放在快捷方式 前面,我没找到是哪控制的.
改完开始菜单就弄桌面快捷方(就是一开机桌面上那几个默认的是短信,联系人,日程和纸牌).设定这个的注册表位置是 HKEY_CURRENT_USERSOFWAREMicrosoftShellStartMRU是修改里面的InitialOrder,方法和 前面修改开始菜单一样的,不过可以加入Start Menu下子文件的快捷方式了.
16. 修改注册表设置背光常开
进注册表里面的Current User下面有一个Control Panel，再下面有一个BackLightTimeout，里面有两个值，一个是Battery，一个是ACXXX，这两个值管的是使用电池时背光点亮 时间和使用交流电充电时背光点亮时间，单位使用的是毫秒，你要是想设置成背光亮十分钟，那你就要把值写成600000。这样你下次给朋友做演示放MTV的 时候你的SP就不会半路关掉背放让你摸黑看MTV了，甚至半夜色你拿它出来当手电筒都没问题！！
17. 自己来定义右软键
修改健值
HKEY_CURRENT_USERSoftwareMicrosofthomekeys113
Default = 右键程序名称（在这里可以随便写自己喜欢的，我把自己的名添上了，哈哈）
Open = StoragewindowsStart Menu所需的程序快捷方式名称.lnk
18. WM6系统解锁
HKEY_LOCAL_MACHINESecurityPoliciesPolicies
00001001: 2改为1
00001005: 16改为40
19. 修改紧急号码
在注册表找到HKEY_LOCAL_MACHINESecurityECallWithoutSIM，把List的值改为110之类的
在注册表找到HKEY_LOCAL_MACHINESecurityECallWithSIM，把List的值改为110之类的
20. 取消在与电脑连接后每 5 分钟自动同步的功能只要修改以下注册表值来解决................  [HKEY_LOCAL_MACHINESystem ActiveSyncEngines{176<a href="http://product.cnmo.com/cell_phone/index156994.shtml">F4</a>FFD-
F20C- 4bd4-BDD7- 01D0726C567B}Settings]"SyncAfterTimeWhenCradled"将 5 改为 0
取消在与电脑连接后每 5 分钟自动同步,将 5 改为 0,就达到不自动同步的效果!
21. 开始菜单九宫改列表
HKEY_CURRENT_USERSoftwareMicrosoftShellStartMenu
1代表9宫格
0代表列表
22. 日历键改为别的程序的热键的办法：
[HKEY_CURRENT_USER/software/Microsoft/Today/keys下的112，和113。
112对应左键，113对应右键
23. 开关机动画<a href="http://blog.cnmo.com/">音乐</a>修改
HKEY_LOCAL_MACHINESoftwareMotorolaSplashAnimationStartup
HKEY_LOCAL_MACHINESoftwareMotorolaSplashAnimationShutdown
