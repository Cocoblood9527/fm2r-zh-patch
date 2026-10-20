# 前线任务2 重制版 · 繁中重译补丁 v1.0.0

PC 版《FRONT MISSION 2 Remake》出厂自带的繁体中文是机翻。本补丁在运行时把游戏 `zh`
语言列的译文整体替换成重译版本,**不修改游戏本体任何文件**。

- 平台:Windows x64(Mono 脚本后端,BepInEx 5)
- 重译以**日文原文**为准,术语已全表统一;输出为台湾用词的繁体中文
- 与同系列的 [fm1r-zh-patch](https://github.com/Cocoblood9527/fm1r-zh-patch)、
  [fm3r-zh-patch](https://github.com/Cocoblood9527/fm3r-zh-patch) 同一套做法

## 下载与安装

**下载 Releases 里的 `FM2R-ZH-Bundle-win64.zip`**(约 1.4MB)。包内已含 BepInEx 5,
不需要另外下载任何东西;本作是 Mono 架构,首次启动**不需要联网、也不会卡几分钟**。

1. 确认游戏本体能正常启动。
2. 把 zip 里**全部内容**复制到游戏根目录(与 `Front Mission 2 Remake.exe` 同级),
   完成后该层应出现 `BepInEx\`、`doorstop_config.ini`、`winhttp.dll`。
3. **把游戏语言切到繁体中文**,否则画面不会变化:
   Steam 库 → 右键游戏 → 内容 → 语言 → 繁體中文(或游戏内语言设定后重开游戏)。

已经自己装好 BepInEx 5 的人,也可以只用本仓库的 `release/FM2RZhPatch/`,
把整个 `FM2RZhPatch` 文件夹放进 `BepInEx/plugins/`。

## 确认补丁生效

打开 `BepInEx\LogOutput.log`,搜 `FM2 Chinese Re-translation`,应看到:

```
Loading [FM2 Chinese Re-translation 1.0.0]
FM2 Chinese Re-translation v1.0.0: loaded 9894 overrides from ...override.bin
source #1: 12360 terms, column 8, 9894 newly applied (unique 9894/9894)
glyph probe prepared: 2133 distinct non-ASCII characters
glyphs: 'NotoSansTC-Regular Dynamic' renders all 2133 characters
```

判定标准:

- `loaded` 后的数字等于 **9894**,对不上就是表没读对(多半是插件目录层级放错)。
- `newly applied` 应大于 0;`column` 是中文列索引(本作中文列为 8)。
- 出现 `renders all N characters` 才不会看到□方框。本补丁不改动游戏字体。
- `BepInEx\ErrorLog.log` 应为 0 字节。

## 覆盖范围

| | |
| --- | --- |
| 全量词条 | 12,360 |
| 本补丁替换 | 9,894 |
| 打包时被拒 | 0 |
| 未重译,保持出厂 | 2,466 |

保持出厂的 2,466 条里,绝大多数是型号名、BBS 账号、人名等**出厂已经正确**的行
(例如 `ガスト５０３Ｂ` 的 `Gust-503B`);另有 6 条日文原文本身就是空的占位键,无内容可译。

**最需要留意的是版式**:713 条译文的换行数与出厂不同(其中 680 条是按日文原文补回断行,
出厂把日文的硬换行压平了),另有 113 条明显长于日文原文 —— 其中 72 条是可滚动的
论坛内文,不影响版面;其余接近对话框两行上限(约 26–32 个全形字),碰到被裁的地方
请对照日文原文判断。

## 术语改动(节选)

出厂机翻把系列术语译错或混用,本补丁按日文与台湾用词统一:

`戰機`→**機甲**(ヴァンツァー,避免与真正的战斗机混淆)、`飛行員`→**駕駛員**、
`機身`→**軀幹**、`飛機棚`→**機庫**、`有效分值`→**行動點**、`記錄`→**超頻**、
`沖床`→**拳**、`鉤爪`→**指虎**、`加農炮`→**加農砲**、`獵槍`→**霰彈槍**、
`導彈`→**飛彈**、`近身搏鬥`→**格鬥**、`調遣`→**移動**、`物件`→**物品**、
`數據`→**資料**、`設置`→**設定**、`網絡`→**網路**、`位置`(address)→**位址**、
`婆羅洲`→**Bornea**、`航母`→**制海艦**、`上尉/上校/中校`→**大尉/大佐/中佐**、
`上將`(将軍)→**將軍**、`修理/恢復`→**修復包/復原包**。
人名与机体型号保留拉丁字母(Ash、Lisa、Ven、Fenrir、Robust-1A …),地名国名音译
(阿洛德什),`U.S.N.` 依日文写法而非官方英文的 `U.C.S.`。

## 卸载

删除游戏根目录下的 `BepInEx`、`doorstop_config.ini`、`winhttp.dll`、`.doorstop_version`、
`changelog.txt`。游戏本体未被改动,删掉即完全还原。

## 说明

- 本仓库与分发包**不含任何游戏文件**,也不含游戏原文:提取与打包工具、逐条携带
  日文/英文原文的译文对照表都留在构建机上,不随仓库分发。
- 译文表以 `override.bin` 发布而非明文:22 字节头(魔数/长度/种子/校验和)+ 密钥流混淆的
  UTF-8 表,插件在内存中还原并校验。这是避免整张表被随手取走的混淆,**不是加密**。
- 调试用的明文导出开关(`BepInEx\config\FM2RZhPatch.cfg` 的 `DumpSources`)默认为 `false`,
  请保持关闭。
- 译文是对游戏文本的转换成果,供已合法持有本游戏的玩家个人使用。
- 游戏更新后 I2 Localization 的语言列索引可能变化,导致插件写错列,需要重新构建。
- 尚未在 Windows 真机验证注入(构建于 macOS 完成,交叉编译 net472)。若日志与上面的
  判定标准不符,请把 `LogOutput.log` 的相关行贴到 Issues。

## 许可

插件代码与本仓库文件采用 [MIT](LICENSE)。游戏本体、游戏内原始文本以及译文所派生的
原始内容仍归各自权利人所有。
