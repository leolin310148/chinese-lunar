# 命理基本的查詢

![npm](https://img.shields.io/npm/v/@tony801015/chinese-lunar)
![npm](https://img.shields.io/npm/dm/@tony801015/chinese-lunar)
[![Build Status](https://travis-ci.org/tony801015/chinese-lunar.svg?branch=master)](https://travis-ci.org/tony801015/chinese-lunar)
[![Coverage Status](https://coveralls.io/repos/github/tony801015/chinese-lunar/badge.svg?branch=master)](https://coveralls.io/github/tony801015/chinese-lunar?branch=master)

目前已提供`年柱`,`月柱`,`日柱`,`時柱`,`農曆月`,`農曆日`,`節氣`,`星期`,`生肖`,`星座`的資訊

# ChangeLog

- 2020/01/18 `0.13.0` 版本提供`時`讓八字有更精準的計算。底下的`特殊方法`有介紹八字計算，歡迎大家試算看看唷～
- 2020/01/08 `0.12.1-beta`版本提供更簡單的使用方式，預設當前時間，也可以自訂自己使用的時間。
- 2019/10/24 `0.9.0`版本提供了此年的農曆中每個月有多少天`getLunarPerMonthHasDays`，這裡可以搭配`0.6.4`版推出的閏月是哪一天來應用。
- 2019/10/23 `0.8.0`版本提供了`星座`，可以從`.getJson()`的`constellation`property 拿到
- 2019/10/23 `0.8.1`版本修復十神，十神需提供使用者出生的年柱做搭配
- 2019/10/21 `0.7.0`版本提供了更長的範圍，從 1956 到 1900 補齊囉～接下來應該就會再往 2050 年之後邁進
- 2019/10/19 `0.6.4`版本提供了此年的閏月是哪一個月份的查詢，新增在`AdvancedLunar`。
- 2019/10/18 `0.6.2`版本提供了十神的查詢，新增在`ApplicationLunar`，所以要使用此方法需 new ApplicationLunar()。
- 2019/10/17 `0.6.0`版本提供了`生肖`的查詢。
- 2019/10/16 `0.5.0`版本提供了`.getJson()`的方法讓大家可以方便取得所有資訊。

# 使用範例

```
npm i @tony801015/chinese-lunar -S
```

### 預設使用方式

```js
const lunar = require("@tony801015/chinese-lunar");
console.log(lunar().getJson()); // 抓取目前的年,月,日
```

### 自定日期

```js
const lunar = require("@tony801015/chinese-lunar");
console.log(lunar("2020", "01", "09").getJson()); // 抓取目前的年,月,日
```

### 取得參數

```js
const lunar = require("@tony801015/chinese-lunar");
const data = lunar("2020", "01", "09").getJson();
console.log(data.year); // 2020
console.log(data.week); // 4
console.log(data.constellation); // 魔羯座
```

### 提供特殊方法
#### setTime() 自訂時間
> 如果沒有輸入，程式會抓取當前時間
```js
const lunar = require("@tony801015/chinese-lunar");
const data = lunar('2021', '02', '13')
  .setTime('00')
  .getJson();
console.log(data.chineseTime); // 庚子
```
#### setChineseAge() 自訂出生年(天干地支)
> 如果沒有輸入程式會顯示提醒 `請輸入年齡`
```js
const lunar = require("@tony801015/chinese-lunar");
const data = lunar('2021', '02', '13') // 出生年月日
  .setTime('00') // 出生時
  .setChineseAge('壬子') // 出生年
  .getJson();
console.log(data.chineseYearTenGod); // 印
console.log(data.chineseMonthTenGod); // ㄗ
console.log(data.chineseDayTenGod); // 比
console.log(data.chineseTimeTenGod); // ㄗ

// 這樣簡單的八字計算就出來囉。 歡迎自己算算看唷～
console.log(`年=> ${data.chineseYear}, 十神=> ${data.chineseYearTenGod}`); // 年=> 辛丑, 十神=> 印
console.log(`月=> ${data.chineseMonth}, 十神=> ${data.chineseMonthTenGod}`); // 月=> 庚寅, 十神=> ㄗ
console.log(`日=> ${data.chineseDay}, 十神=> ${data.chineseDayTenGod}`); // 日=> 壬辰, 十神=> 比
console.log(`時=> ${data.chineseTime}, 十神=> ${data.chineseTimeTenGod}`); // 時=> 庚子, 十神=> ㄗ
```

|      中文名稱      |       參數名稱       |  型態   |                                                範例                                                | 備註 | 
| :----------------: | :------------------: | :-----: | :------------------------------------------------------------------------------------------------: | :--: | 
|         年         |         year         | string  |                                                2020                                                | |
|         月         |        month         | string  |                                                 01                                                 ||
|         日         |         day          | string  |                                                 09                                                 ||
|        節氣        |      solarTerms      | string  |                                                小寒                                                ||
|       農曆月       |      lunarMonth      | string  |                                                腊月                                                ||
|       農曆日       |       lunarDay       | string  |                                                十五                                                ||
|     年柱     |     chineseYear      | string  |                                                己亥                                                ||
|     月柱     |     chineseMonth     | string  |                                                丁丑                                                ||
|     日柱    |      chineseDay      | string  |                                                辛亥                                                ||
|     時柱     |     chineseTime     |  string  | 戊子 | 需要先 `setTime()` 如果沒有就會是目前的時間 |
|     年柱十神     |     chineseYearTenGod     |  string  | 殺 |需要先 `setChineseAge()`|
|     月柱十神     |     chineseMonthTenGod     |  string  | 印 |需要先 `setChineseAge()`|
|     日柱十神     |     chineseDayTenGod     |  string  | ㄗ |需要先 `setChineseAge()`|
|     時柱十神     |     chineseTimeTenGod     |  string  | 比 |需要先 `setChineseAge()`|
|     時柱十神清單     |     chineseTimesTenGod     |  array  | [ 'ㄗ', '印', '比', '劫', '食', '傷', '才', '財', '殺', '官', 'ㄗ', '印' ] |需要先 `setChineseAge()`|
|     時柱清單     |     chineseTimes      |  array  | [ '戊子', '己丑', '庚寅', '辛卯', '壬辰', '癸巳', '甲午', '乙未', '丙申', '丁酉', '戊戌', '己亥' ] ||
|        星期        |         week         | string  |                                                 4                                                  ||
|        生肖        |        animal        | string  |                                                 鼠                                                 ||
|        星座        |    constellation     | string  |                                               魔羯座                                               ||
| 國曆二月是否有閏月 |      chineseFeb      | boolean |                                                true                                                ||
|        登貴        |       dengGui        | string  |                                                戌午                                                ||
|     農曆潤幾月     |      leapMonth       | number  |                                                 4                                                  ||
|   農曆每月有幾日   | lunarPerMonthHasDays |  array  |                [ '29','30','30','30','29','30','29','29','30','29','30','29','30' ]                ||

# 分享

設定檔 `config.js` 裡面有一些整理過的資訊，希望可以幫助到大家對於命理上的研究。歡迎大家找我討論～

# 注意事項

- 目前計算的時間以 1900 年開始至 2050 年，1900 以前的都無法計算。

# 未來規劃

未來會再增加

- 星座 `BasicLunar` 2019/10/23 完成 `0.8.0`
- 此年的閏月是幾月 `AdvancedLunar` 2019/10/19 完成 `0.6.4`
- 此年的農曆中每個月有多少天 `AdvancedLunar` 2019/10/24 完成 `0.9.0`
- 農曆日期的差距有幾天 `ApplicationLunar`
- 十神的查詢 `ApplicationLunar` 2019/10/17 完成 `0.6.2`
- 提供時間的輸入，在八字裡面其實就是把`年`,`月`,`日`,`時`轉成`年柱`,`月柱`,`日柱`,`時柱`，因此要把八字更精準推出命理相關的數據，需要`時`的協助囉。 2020/01/18 完成 `0.13.0`
- 輸入農曆轉換成國曆
- 製作前端使用js
- 製作萬年曆
- 查詢農曆年的API
