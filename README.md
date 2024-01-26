# PalWorld-Save-Movement-Complete-Tutorio
Welcome anyone can translate this Tutorio in other Languages


# 幻兽帕鲁存档转移完全教程


> ### :warning: 
>
> 此转移操作可能会导致你的存档出现如下问题：
> 被暗巫猫带走。
> 被炸弹鸟炸掉。
> 我仍然强烈建议你在进行任何操作之前进行充分的备份。防患于未然最重要。保持乐观和平和的心态，同时做好最坏的准备。跟着我一步一步完成这项工作。


##　前言

本教程面向那些拥有探索精神、一定的计算机技术经验，并且最重要的——具备耐心的玩家。我将一步步引导你完成幻兽帕鲁存档的转移过程。

## 准备工作

在开始之前，请确保你已经准备好以下几项：

1. 老主机的存档 - 你需要从你的老主机中获取幻兽帕鲁的存档文件。这是转移过程中不可或缺的一部分。

2. 新云服务器 - 准备一个新的云服务器，用于存放和运行幻兽帕鲁的新存档。

3. 存档文件位置 - 在你的服务器文件夹下找到 `Pal\Saved\SaveGames\<random_numbers> `路径，保存。个人建议将整个 `Saved` 文件夹打包，以便进行未来的操作。

4. 下载压缩包 - 我会提供一个打包好的压缩包，里面包含了进行存档转移所需的所有必要文件。

5. 解压到合适位置 - 将压缩包解压到一个合适的位置。例如，你可以创建一个名为 mirage_save 的文件夹，用于存放解压后的文件。

6. 确认你现有的存档的服务端

 - LinuxServer Manual Install with Official Guide
 - LinuxServer 服务商面板服
 - WinServer 与 steamcmd
 - WinServer 与 steamclient
 - Windows 合作模式

请确保以上步骤都已经完成，然后我们可以继续下一部分的内容。

##　确定自己的存档玩家PID来源

PalWorld的玩家PID依照两点来确定（我的未证实的经验）

1. 玩家的steamID，个人资料的ID
2. **服务器的APPID**（重点）

- 对于windows用户来说，你们有三种appid
 - - 未加载steam库导致的无ID
 - - steamcmd 安装独立客户端的ID = 1623730
 - - steamclient 安装独立客户端的ID = 2394010
 - - 合作模式的ID = 2394010
- 对于Linux用户来说，你们有两种appid
 - - 未加载steamclient.so导致的无ID
 - - 按照官方教程安装的ID = 2394010

>  ID可以看服务端的Output 会输出 `SteamAPPID = <NUMBER>`



## 服务器APPID类型



- 无ID

- 1623730 = 幻兽帕鲁游戏

- 2394010 = 幻兽帕鲁独立服务器

  

  >  :warning: 未经验证的报告显示1623730 与 2394010 会产生相同的效果，也就是其可以等价



## 服务器间的转移



1. 确定自己转移前后的服务器APPID保持不变。

2. 登录服务器以创建一个新世界。

3. **关闭服务器。**

4. 删除`PalServer\Pal\Saved\SaveGames\0\`

5. - 对于Linux：
   - - 在`PalServer\Pal\Saved\Config\LinuxServer\GameUserSettings.ini`文件中，更改 以 `DedicatedServerName` 匹配保存的文件夹名称。例如，如果保存的文件夹名称为 `2E85FD38BAA792EB1D4C09386F3A3CDA` ，则 `DedicatedServerName` 更改为 `DedicatedServerName=2E85FD38BAA792EB1D4C09386F3A3CDA` 。
   - 对于Windows：
   - - 在`PalServer\Pal\Saved\Config\WindowsServer\GameUserSettings.ini`文件中，更改 以 `DedicatedServerName` 匹配保存的文件夹名称。例如，如果保存的文件夹名称为 `2E85FD38BAA792EB1D4C09386F3A3CDA` ，则 `DedicatedServerName` 更改为 `DedicatedServerName=2E85FD38BAA792EB1D4C09386F3A3CDA` 。`

6. 将你的存档复制到PalServer\Pal\Saved\SaveGames\0\下。

> 类似PalServer\Pal\Saved\SaveGames\0\\<your_save_here>\

7. 删除 `PalServer\Pal\Saved\SaveGames\0\<your_save_here>\WorldOption.sav` （**可能没有，非常正常，没有不需要删除**）以允许修改 `PalWorldSettings.ini` .（会导致玩家丢失地图以及重生点）

8. 登录服务器，验证是否转移成功，如果转移不成功，回到[确定自己的存档玩家PID来源](#确定自己的存档玩家PID来源)。



​	存档应该正常迁移了。

## 从合作模式迁移到服务器



合作模式与服务器间的转移最大的区别是有关主机存档的迁移。对于合作模式来说，主机玩家在本地存档里的ID是`00000000000000000000000000000001.sav`。

于是帕鲁Discord有大神写了一个python脚本，用来转换存档。地址如下

[幻兽帕鲁主机存档修复](https://github.com/xNul/palworld-host-save-fix)



步骤如下。



###　在开始之前

1. 下载github的python，[palworld-host-save-fix](https://github.com/xNul/palworld-host-save-fix)，在我打包的文件中也有。
2. 安装python>3.10
3. 获取[uesave-rs](https://github.com/trumank/uesave-rs)，在我打包的文件中也有，名字叫uesave.exe。



## 说明

python脚本

> :cactus: GUID = PID的十六进制版本，存档文件的文件名是GUID



Command: 命令：
`python fix-host-save.py <uesave.exe> <save_path> <new_guid> <old_guid>`

`<uesave.exe>` - uesave.exe 的路径
`<save_path>` - 保存文件夹的路径
`<new_guid>` - 新服务器上Player的 GUID
`<old_guid>` - 旧服务器中Player的 GUID



Example: 例：
`python fix-host-save.py "C:\Users\John\.cargo\bin\uesave.exe" "C:\Users\John\Desktop\my_temporary_folder\2E85FD38BAA792EB1D4C09386F3A3CDA" 6E80B1A6000000000000000000000000 00000000000000000000000000000001`



> 此脚本的作用是将一个`GUID.sav`迁移到另一个`GUID.sav`，同时修改`Level.sav`以保证数据一致性。



##　开始



### PART I:



1. 确定自己转移前后的服务器APPID保持不变。
2. 登录服务器以创建一个新世界。
3. **关闭服务器。**
4. 删除`PalServer\Pal\Saved\SaveGames\0\`
5. - 对于Linux：
   - - 在`PalServer\Pal\Saved\Config\LinuxServer\GameUserSettings.ini`文件中，更改 以 `DedicatedServerName` 匹配保存的文件夹名称。例如，如果保存的文件夹名称为 `2E85FD38BAA792EB1D4C09386F3A3CDA` ，则 `DedicatedServerName` 更改为 `DedicatedServerName=2E85FD38BAA792EB1D4C09386F3A3CDA` 。
   - 对于Windows：
   - - 在`PalServer\Pal\Saved\Config\WindowsServer\GameUserSettings.ini`文件中，更改 以 `DedicatedServerName` 匹配保存的文件夹名称。例如，如果保存的文件夹名称为 `2E85FD38BAA792EB1D4C09386F3A3CDA` ，则 `DedicatedServerName` 更改为 `DedicatedServerName=2E85FD38BAA792EB1D4C09386F3A3CDA` 。`

6. 将你的存档复制到PalServer\Pal\Saved\SaveGames\0\下。

> 类似PalServer\Pal\Saved\SaveGames\0\\<your_save_here>\

7. 删除 `PalServer\Pal\Saved\SaveGames\0\<your_save_here>\WorldOption.sav` （**可能没有，非常正常，没有不需要删除**）以允许修改 `PalWorldSettings.ini` .（会导致玩家丢失地图以及重生点）

8. **请让你的朋友登录服务器，验证是否转移成功，如果转移不成功，回到[确定自己的存档玩家PID来源](#确定自己的存档玩家PID来源)。**

## PART II



1. 如果成功，现在开始解决你的作为主机的存档问题。

2. 请你登录服务器，创建角色，并开启一个存档点。

3. 这时候你可以看到在`PalServer\Pal\Saved\SaveGames\0\<your_save_here>\`文件夹下多出一个新的`<GUID>.sav`存档，这个存档就是你的存档。

4. 关闭服务器，然后将整个专用服务器存档 `PalServer\Pal\Saved\SaveGames\0\<your_save_here>` （必须是带有合作主机新角色的存档！）复制到临时文件夹中，并记住临时文件夹的路径，因为运行脚本需要它。

5. **备份你的存档！**（除非你想和帕鲁永别）

6. 使用`fix-host-save.py`脚本将你的旧存档`00000000000000000000000000000001.sav`替换成`<New_GUID>.sav`。

7. 将存档从临时文件夹复制回专用服务器。

8. 启动服务器,你应该能正常进入游戏了。到此，你的存档已经成功迁移。

9. 如果你的伙伴们不再为你攻击或在基地里工作，请按照[伙伴错误]()解决方法修复它们。





## 将存档从合作模式迁移到另一个合作模式/从主机迁移到合作模式

待更新。你或许可以从[从合作模式迁移到服务器](##从合作模式迁移到服务器) 获取启发。可能明天更新，也可能后天更新。



技术上是可以做到的，我已经成功很多次了

**如果你成功了，欢迎你也写教程发出来。社区因你而精彩。**



## 已知bug

### 帕鲁错误

玩家拥有的帕鲁不会在基地做任何事情，或者被举起。这可能是由于帕鲁没有正确被识别为你的帕鲁。



解决方法：在新服务器上，在保存修复后，抛弃帕鲁并重新捕获帕鲁。


如果你还有不懂的地方，可以加入QQ群咨询我，我是群主



<img src="https://github.com/GalileoFe/PalWorld-Save-Movement-Complete-Tutorio/assets/138156577/1296a517-9958-44ea-be73-a2433d455544" width="200">


