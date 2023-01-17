# **CrystalFrostwork For SM8250**

------------

**目录**

- [内核介绍](#内核介绍)
- [内核特性](#内核特性)
- [内测渠道](#内测渠道)
- [安装方法](#安装方法)
- [相关声明](#相关声明)
- [常见问题](#常见问题)
- [已知问题](#已知问题)
- [高级用法](#高级用法)
- [下载链接](#下载链接)
- [更新日志](#更新日志)

------------

## 内核介绍
- 适用ROM：基于MIUI的Android 11-13系统
- 适用机型：小米10、小米10 Pro、小米10 Ultra、红米K30 Pro、红米K30s Ultra
- 内核版本：4.19.269（CrystalFrostwork Build 509 Release)
- 开发者：阿菌•未霜

## 内核特性
- CPU调度器：powersave、performance、schedutil（默认）
- I/O调度器：cfq（默认）
- TCP拥塞算法：reno、lia、olia（默认）
- 移植上游MGLRU v15，降低内存开销，提升回收效率。
- 移植上游DAMON，优化内存回收。
- 内核支持ExFAT、NTFS3、EROFS文件系统。
- 支持自定义充电电流，USB Type-C口最大输入电流不限制，具体方法请见下文高级用法。
- 支持电压查看，可修改文件选择支持EX Kernel Manager或Kernel Adiutor的接口，具体方法请见下文高级用法。
- 解锁电池最大输入电流限制。
- 支持唤醒锁管理。
- 支持Fsync控制，默认开启，可通过内核管理软件关闭。
- 移植来自Linux 5.2内核上的lzo-rle压缩算法。
- 移植来自Linux 5.15内核上的LRNG（Linux随机数生成器），优化随机数生成速度
- 同步上游最新ZSTD源码，并作为ZRAM压缩算法，提高IO速度和压缩率。
- 支持ZRAM自动回写。
- 支持屏幕最低亮度控制。
- 自带内核级别温控，替换小米官方极为不合理的温控。
- 电池充电降速温度阈值提高至 55℃。
- 优化F2FS文件系统的垃圾回收（GC）功能，解决文件系统掉速问题。
- 移除了小米官方在 ION 中设置的保留内存（大约节约 400M-500M 的可用内存）。
- 禁用了幽灵漏洞、熔断措施安全补丁，恢复完整的 CPU 性能。
- 移除小核低于691MHz的频率，提高能效。
- 满血快充，保证全程充电最大功率。
- 破解小米私有快充协议限制，支持绝大多数带PPS协议的充电器开启Mi Turbo Charge。
- 支持某些快充协议设计不严谨的PPS充电器开启PPS快充。
- 加入为MIUI特别优化的WALT调度器。
- 加入虚假的SELinux严格模式，禁用SELinux的同时不会被第三方软件检测出SELinux处于宽容模式。
- 支持大容量电池（破解锁容）
- 支持未通过验证的电池启用快充（尽管系统可能会弹出提示）
- 更强的后台驻留能力（需要开启增强后台功能）

&emsp;&emsp;*更多特性，请下载体验*

## 内测渠道
- 本内核公开版完全免费，无任何功能上的限制，但公开版~~随缘更新~~更新速度较慢，需要更快体验新功能以及稳定的更新保证可以加入内测群，**车费20**。
- 内测群号：852535850（[或点击这里直接加入群聊【CrystalFrostwork SM8250内核群】](https://jq.qq.com/?_wv=1027&k=Pj3soRd7 "或点击这里直接加入群聊【CrystalFrostwork SM8250内核群】")）
- 付费渠道（左微信，右支付宝）：
![付款渠道（左微信，右支付宝）](https://gitea.com/Mandi-Sa/CrystalFrostwork-Archive/raw/branch/main/%E4%BB%98%E6%AC%BE%E6%B8%A0%E9%81%93.jpg "付款渠道（左微信右支付宝）")
- 付款完成后，请私聊管理（QQ：3069667229），并将付款记录发送给管理，管理确认后将拉入群聊。

## 安装方法
1. 解锁Bootloader，刷入TWRP（建议使用SK大佬的TWRP），重启进入Recovery。
2. 刷入Magisk（建议）。
3. 安装内核**卡刷包**（不要再问我为什么面具或软件里刷不进之类的~~聪明~~问题了……）
4. 重启
- **安装完内核第一次重启可能会花费较长时间，请耐心等待！**

## 相关声明
1. 使用此内核具有一定的风险性，包括但不限于：**主板硬件损坏、数据丢失、失去保修等**，本人不承担刷入此内核所带来的任何直接或间接损失和任何后果。若不同意本条款请不要下载使用！一旦内核刷入手机则代表已同意本条款！
2. 此内核带有高速快充的功能，比其他大多数内核充电电流更大，且内核温控阈值很高，因此使用过程中可能会产生大量的热量，请注意设备散热。若无法接受请不要刷入使用，或配合其他第三方软件（如Scene）限制充电电流使用。

## 常见问题
1. 此内核我只能保证在基于MIUI的Android 11和Android 12的官方系统上能够正常运行，其他的任何ROM（如官改、类原生等）所可能出现的问题，本人不保证能解决和任何的技术支持。
2. 为什么内核刷不进去/刷入错误1？
	看一下有没有写的支持你的机型，或者使用我推荐的Recovery版本。
3. 能不能做下某某机型/某某处理器的内核？
	精力有限，暂时没有考虑做其他处理器的内核，不要再问我这个问题了。
4. 有没有手把手的小白教程？
	不建议小白刷内核。
5. 能不能教我写内核？
	我没有这个时间，也没有这个义务。酷安话题**#XDA 干货挖掘计划#**里面有，自己多看看。
6. 为什么会出现充电断冲的问题？
	1. 如果使用的是第三方充电器，则说明你的充电器可能无法达到Mi Turbo Charge的要求，执行下面的命令禁用内核对于小米私有协议的破解：

	`echo 0 >/sys/crystalfrostwork/charge_control/pd/force_pd_verifed`

	若要恢复破解，则：

	`echo 1 >/sys/crystalfrostwork/charge_control/pd/force_pd_verifed`

	2. 如果是官方充电器……那可能就是线的问题了吧……
7. 红米K30 Pro、红米K30s Ultra可直接写入charge_full节点实现手动解容，而小米10、小米10 Pro、小米10 Ultra由于电池容量计算不由内核、系统控制（自带电量计芯片bq27z561）因此不能手动设置容量，必须等电量计芯片长时间使用自动校正容量才能达到解容的目的。

## 已知问题
1. 呼吸灯无效或乱闪。

	解决方法：无，官方未更新源码。

2. ZRAM大小/压缩算法不能更改/关闭。

	解决方法：无，内核设定如此，不允许关闭ZRAM。

## 高级用法
*本节内容需要有一定的基础，看不懂的请跳过，不做额外的技术支持*

### 自定义充电电流
1. 打开X-plore文件管理器
2. 找到位置`/sys/crystalfrostwork/charge_control`

#### battery文件夹
- bypass_verify：禁用电池验证，强制认为电池为官方认证电池。

#### hvdcp文件夹
- qc2_current_ma：QC2.0充电协议下，Type-C口最大允许输入的电流。
- qc3_current_ma：QC3.0充电协议下，Type-C口最大允许输入的电流。

#### legacy文件夹
- cdp_current_ma：CDP（Charging Downstream Port）充电协议下，USB最大输入电流。
  - *通常手机连接不支持快充协议的充电器时，协商此协议。*
- dcp_current_ma：DCP（Dedicated Charging Port）充电协议下，USB最大输入电流。
- sdp_current_ma：SDP（Standard Downstream Port）充电协议下，USB最大输入电流。
  - *通常手机USB连接电脑时，协商次协议。*
- input_volt_limit_mv：进行CDP、DCP、SDP充电时，USB接口允许的最低电压。
  - *为了防止电流过大而触发电源输出过载保护，当检测到USB接口上的电压低于这个值时，将会自动降低输入电流以确保最终的USB接口上的电压不会低于所设置的电压。电压保护阈值设置越低可能达到的充电电流越高，同时触发电源输出过流保护的可能性越大。*
  - *仅小米10 Ultra支持此功能*

#### pd文件夹
- force_pd_verifed：强制认为所有的PD充电器为已认证状态（破解小米私有充电协议）。
- ignore_current_negotiate：忽略PD充电器报告的最大允许电流上限，强制使用定义的电流。
- ignore_incorrect_state：忽略某些比较旧的PD充电器在协议上存在的问题，导致协议协商失败。（可能能解决某些PD充电器无法正常充电或充电缓慢的问题）
- ignore_usbpd_hard_reset：忽略充电器发来的硬重置信号。（可能能解决某些情况下断冲的问题）
- overwrite_pps_current：强制使用pps_current_ma中定义的电流覆盖充电器汇报PPS挡位所支持的电流。
- pd_current_ma：PD充电协议下，Type-C口最大允许输入的电流。
- pd_voltage_level：PD充电协议下，最大允许使用的电压档位
	- 1：5V
	- 2：9V
	- 3：12V
	- 4：15V
	- 5：20V
- pps_current_ma：PPS充电协议下，Type-C口最大允许输入的电流。
- unverifed_current_ma：当充电器未通过小米认证时，Type-C口最大允许输入的电流。
- vbus_voltage_mv：Type-C最大允许电压（单位mV)。


### 文件管理
1. 打开X-plore文件管理器。
2. 找到位置`/sys/crystalfrostwork/file_manager`
文件夹内有三个文件夹，其中block为阻止特定进程打开某个文件，overwrite为对某个进程打开某个文件，用特定的文件代替。

#### block文件夹
- config：配置文件
 - 配置文件格式：`进程名,文件路径`，支持通配符"\*"，其中“,”为分隔符。
 - 下面有几个例子：
   - `*,/vendor/etc/thermal*`：禁止所有的进程读取/vendor/etc/下，thermal开头的文件名的文件。
   - `com.tencent.mobileqq,/sdcard/123.txt`：禁止QQ打开/sdcard/123.txt这个文件。
- status：当前被拦截的次数统计。

#### overwrite文件夹
- config：配置文件
 - 配置文件格式：`进程名,被重定向的文件路径,用于重定向的文件路径`，仅支持进程名使用通配符"\*"，其中“,”为分隔符。
 - 下面有几个例子：
   - `*,/vendor/etc/thermal-engine.conf,/sdcard/thermal/thermal-engine.conf`：将所有进程对于打开/vendor/etc/thermal-engine.conf的请求，重定向到/sdcard/thermal/thermal-engine.conf文件上。
   - `com.tencent.mobileqq,/sdcard/123.txt,/sdcard/456.txt`：将QQ打开/sdcard/123.txt的请求，重定向到/sdcard/456.txt文件上。
- status：当前被重定向的次数统计。

### 电压查看配置文件切换
1. 打开X-plore文件管理器。
2. 找到位置`/sys/crystalfrostwork/voltage_viewer`
3. 设置profile文件的值，其中：
 - 0：关闭电压显示功能，关闭当设置为此值时，任何软件都无法查看电压。
 - 1：兼容Kernel Adiutor的接口，显示最为完整，但EX Kernel Manager会有部分显示错误。
 - 2：兼容Kernel Adiutor和EX Kernel Manager的接口，但显示的信息较少。
4. 修改之后保存及时生效，若软件读取没有变化，请重启软件。

**警告：电压仅允许查看，请不要尝试写入，否则可能会造成不可预料的后果！（如系统崩溃）**

### 增强后台
- 在MIUI上，除了AOSP的LMKD低内存杀手之外，还有额外的服务（MiuiMemoryService）用于杀后台，导致后台能力下降。
1. 打开X-plore文件管理器
2. 找到文件`/sys/crystalfrostwork/enhanced_background/enabled`
3. 修改文件的值，其中：
 - 0：禁用增强后台功能，后台管理与MIUI官方一致。
 - 1：启用增强后台功能，屏蔽`MiuiMemoryService`服务发出的终止进程信号。（内核默认）
4. 修改之后保存及时生效，重启恢复默认。

### 虚假的SELinux严格模式
1. 打开X-plore文件管理器
2. 找到文件`/sys/crystalfrostwork/fake_selinux/enabled`
3. 修改文件的值，其中：
 - 0：禁用该功能。
 - 1：启用该功能。（内核默认）
4. 修改之后保存及时生效，重启恢复默认。

### ZRAM自动回写
1. 打开X-plore文件管理器。
2. 找到位置`/sys/crystalfrostwork/zram_wbd`
- debug：是否启用模块调试信息输出。（默认：0）
- enable：是否启用该内核模块。（默认：1）
- interval：ZRAM自动回写的间隔（单位：秒，默认：60）
- max_pages：单次回写操作最多回写的页面数量（一个页面大小为4kB，默认：4096）
- min_idle：ZRAM中的页面至少多少秒没有被访问，才允许被回写（默认：1800）
- min_touch：在单次回写间隔中，至少需要有多少秒的用户输入操作才会启动回写（默认：2）
- min_use：ZRAM至少达到多少百分之多少的使用率时，才会允许执行回写操作（默认：25）

## 下载链接
| 版本号 | 文件名 | 文件大小 | 校验和（MD5） | 链接 |
| ------------ | ------------ | ------------ | ------------ | ------------ |
| 509 | CrystalFrostwork-Build-509-For-SM8250-Releases.zip | 22,088,408 字节 | BAFB791EAA2BFBDD771219459A3000C7 | [下载](https://gitea.com/Mandi-Sa/CrystalFrostwork-Archive/raw/branch/kernels/CrystalFrostwork-Build-509-For-SM8250-Releases.zip "下载") |
| 369 | CrystalFrostwork-Build-369-For-SM8250-Releases.zip | 22,793,455 字节 | DC794317F6A4FB4D5C2D844F24F4058D | [下载](https://gitea.com/Mandi-Sa/CrystalFrostwork-Archive/raw/branch/kernels/CrystalFrostwork-Build-369-For-SM8250-Releases.zip "下载") |
| 245 | CrystalFrostwork-Build-245-For-SM8250.zip | 22,760,675 字节 | 4EA0CC3222AAD9BC0302FFF2CA2AE258 | [下载](https://gitea.com/Mandi-Sa/CrystalFrostwork-Archive/raw/branch/kernels/CrystalFrostwork-Build-245-For-SM8250.zip "下载") |

## 更新日志
### Build 509
1. Linux 分支更新至4.19.269
2. 内核基线更新至LA.UM.9.12.r1-15100-SMxx50.QSSI12.0
3. 同步上游F2FS的优化更改以及补丁
4. 支持MIUI14 Android 13
5. 移植上游MGLRU v15并启用，降低内存开销，提升回收效率。
6. 修复刚开机时WLAN无法打开，且概率自动关闭的问题。
7. 修复锁屏状态下亮度过低的问题。
8. 移除多线程kswapd（存在问题且与MGLRU冲突）
9. ZRAM默认大小更改至10G
10. ZRAM默认压缩算法更改至ZSTD
11. 同步上游最新ZSTD源码
12. 内存管理默认参数优化
13. 支持增强后台，防止MIUI杀后台
14. 支持控制SDP、CDP、DCP协议充电电流
15. 移除MPTCP（MultiPathTCP）支持（存在问题）
16. 优化CPU容量分配-容量需求曲线
17. 完善对于小米私有快充协议的破解（UI能显示电量小数了）
18. 修复小米10空载电流过高、耗电的问题
19. 移植上游LRNG（Linux 随机数生成器）v45，优化随机数生成速度
20. 移植上游对ARM64汇编函数的优化，提高内核效率
21. 移植来自华为的LZ4解压汇编代码，提高LZ4解压速度
22. 允许禁用虚假的SELinux严格模式
23. 其他一些可能影响使用的小问题修复

### Build 369
1. Linux 分支更新至4.19.237
2. 内核基线更新至LA.UM.9.12.r1-14000-SMxx50.0
3. 修复WDC闪存设备存在的息屏睡死问题
4. 同步小米12X上的相机修改，支持最新的MIUI13系统（请卸载用于Build 245的相机修复模块）
5. 同步上游F2FS的优化更改以及补丁
6. 修复MIUI Android12系统下，游戏切后台之后被锁帧的BUG
7. 修复系统耗电排行中出现的android.system.suspend@1.0-service进程统计BUG
8. 修复CPU多线程性能异常降低的BUG
9. 修复小米10 Ultra使用官方充电器会导致充电断充的BUG
10. 修复有概率出现应用无响应的BUG
11. 修复随机数发生器的BUG导致VMOS无法使用的BUG
12. 修复可能出现的系统界面随机卡死的BUG
13. 修复WLAN驱动中存在的一些问题
14. 支持红米系列手动电池解容（小米系列电池容量由主板电量计控制，无锁容，多次充放电即可达到自动解容目的）
15. 加入基于DAMON的内存回收功能
16. 加入MPTCP（MultiPathTCP）支持
17. 加入ZRAM DEDUP（重复数据删除）功能，降低内存使用
18. 优化ZRAM重复数据删除HASH列表计算速度，降低HASH重复率
19. 从小米12X的内核源码中导入最新的充电控制功能
20. 从小米12X的内核源码中导入小米对于网络协议的修改
21. 移植最新的震动驱动程序，优化震动效果（仅小米10系列）
22. 加入UFS时钟门动态控制，提高系统流畅度
23. ZRAM压缩、解压\kswapd多线程异步化处理
24. 更新触屏驱动程序固件
25. 优化电量显示，去除小米的虚假电量，使电量显示更精准（如官方内核上100%-99%能用非常久，但10%以下掉电非常快的问题）
26. 优化GPU工作进程，提高渲染效率
27. 加入更快的原生CRC32数据校验
28. 更新WireGuard驱动

### Build 245
1. 初版发布。