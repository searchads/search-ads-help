## Understanding reports 理解报表

要深入了解广告系列的效果，请访问“搜索广告报表”部分。 您可以按日期，广告组或关键字查看，并绘制各种指标：

* Spend 花费
* Taps 点击量
* Conversions 应用下载量
* TTR（tap-through rate）点击转化率
* Average CPA 平均每次下载成本
* Average CPT 平均每次点击成本
* Impressions 展示量
* CR 下载转化率

您也可以按设备过滤数据。

注意：报表不包含应用内购买的数据。此外，搜索广告不支持使用第三方跟踪网址变量。但是，如果您想要跟踪客户的生命周期价值，请考虑实施搜索广告归因API。

您在页面上看到的图表将根据您选择的参数自动更改。 使用其上方的下拉菜单选择指标选项，然后从左侧导航中选择报表类型。

![Reports_CampaignAge_large_2x.jpg](img/Reports_CampaignAge_large_2x.jpg)

**如何查找报表**

要访问“报表”页面，请登录您的帐户。 您将看到“广告系列”页面。 接下来：

* 选择您要查看的广告系列。
* 在广告系列概览页面中，点击报表标签。
* 选择您要查看和过滤详细报表的方式。

**如何阅读报表**

**1）图表视图**

“报表”页面顶部的图表视图为您提供了按日期列出的效果指标的快照。 您可以过滤视图并比较指标，以便深入了解广告系列数据。 注意：日期视图是唯一允许您选择多个指标的视图。

过滤器选项将显示在图表的左上角，一旦应用，将持续显示，直到您删除或更改。 当你调整过滤器，你会立即看到一个新的视觉效果。

![chart-view_large_2x.png](img/chart-view_large_2x.png)

**2）表格视图**

根据您选择的过滤器和指标，表格会合并所选视图中每个组的总计。可用的过滤器取决于您的视图。

![table-view_large_2x.png](img/table-view_large_2x.png)

**性别，年龄和位置报表视图中的“用户保留”（User Withheld)**

如果您未在广告组或广告系列中使用受众群体细分，可能会在报表视图中的年龄，性别或地理位置部分下面显示一个标题为“用户保留”的类别。 这意味着一些看到您的广告的用户已在其设备上启用了“限制广告跟踪”或停用了位置服务。

**年龄范围报表**

按年龄查看报表时，指标会分以下预设年龄组：18-24岁，25-34岁，35-44岁，35-54岁，55-64岁，65岁以上。

**报表视图中的“低量”（Low Volumn）指示器**

某些报表可能会返回“低量”的值。这意味着您请求的数据低于Apple的隐私权阈值。例如，搜索词必须至少达到10次展示，否则搜索词报表中会显示“低量”值。年龄，性别或位置报表需要至少100次展示，然后搜索广告才能显示数值。

---

## Report definitions 报表定义

不确定您在看什么，或找什么？这里有一个您在排序搜索广告效果数据时看到的词和缩略词的指南。

**Impressions 展示量**

您的赞助广告在报表时间段内在App Store搜索结果中显示的次数。

**Taps 点击量**

在报表时间段内用户点击您广告的次数。

**Conversions 下载量**

报表期内由赞助广告产生的下载或重新下载总次数。搜索广告转化的归因有30天的点击转化窗口期。

**TTR 点击转化率**

点击率（TTR）是客户点击您的广告的次数除以您的广告获得的总展示次数。

**CR 下载转化率**

转化率（CR）是一个时段内接收到的转化总数除以同一时段内的总点击数。

**Avg CPA 平均每次转化成本**

平均每次转化费用（CPA）是总支出除以一段时间内获得的转化次数。

**Avg CPT 平均每次点击成本**

平均每次点击成本（CPT）是花费除以一段时间内获得的点击次数。

**Spend 花费**

每个客户点击广告的费用总和。

---

## Attribution API 归因API

**关于搜索广告API**

通过搜索广告归属API，您可以跟踪和归因于来自搜索广告系列的应用下载。很容易准确地测量新获得的用户的生命周期价值和您的广告活动的有效性。

**API优点**

只要在应用程式中加入几行代码，即可轻松了解一段时间内不同客群的价值，以及促成转换的关键词。您可以使用此信息为不同的关键词，广告组和受众群体优化您的CPT和CPA目标。

**API要求**

该应用必须启用搜索广告归因代码才能跟踪归因。

您可以随时为应用启用归因功能，以追踪由搜索广告系列带来的应用下载。

归因仅适用于运行iOS 10或更高版本的用户，并且这些用户点击了搜索广告系列，并在30天内下载了该应用。

**如何实现API**

要启用您的应用归因功能，请按照下列步骤操作：

1. 将iAd框架添加到应用程序的Xcode项目文件中。
2. 在包含您的归因代码的文件中导入iAd头：
  #import <iAd/iAd.h>
3. 检查搜索广告归因，并使用广告系列报表中的结果。

```objective-c
// Check for iOS 10 attribution implementation
if ([[ADClient sharedClient] respondsToSelector:@selector(requestAttributionDetailsWithBlock:)]) { 
NSLog(@"iOS 10 call exists"); 
[[ADClient sharedClient] requestAttributionDetailsWithBlock:^(NSDictionary *attributionDetails, NSError *error) { 
// Look inside of the returned dictionary for all attribution details
NSLog(@"Attribution Dictionary: %@", attributionDetails); 
}];
}
```

以下是来自归因API的响应对象（版本3.1），其中包含广告系列层次结构详细信息，竞价关键字，下载日期和点击日期。

```json
{
"Version3.1" = { 
"iad-attribution" = true;
"iad-org-name" = "Light Right"; 
"iad-campaign-id" = 15292426; 
"iad-campaign-name" = "Light Bright Launch"; 
"iad-conversion-date" = "2016-10-14T17:18:07Z";
"iad-click-date" = "2016-10-14T17:17:00Z";
"iad-adgroup-id" = 15307675; 
"iad-adgroup-name" = "LightRight Launch Group"; 
"iad-keyword" = "light right"; 
}; 
}
```

[查看完整API文档](http://searchads.apple.com/help/pdf/attribution-api.pdf)

---

## Privacy 隐私

**搜索广告和隐私权**

Apple收集的所有搜索广告数据都必须遵守Apple隐私政策，Apple不会将数据出售给第三方。搜索广告不会使用来自其他Apple服务（例如地图，Siri，iMessage和iCloud）的用户个人数据，也不会使用用户设备上的服务和功能（例如健康，HomeKit，电子邮件，联系人和通话记录）中的用户个人数据。

用户还可以通过使用限制广告跟踪功能选择停止接收定向广告。默认情况下，儿童的Apple ID帐户启用限制广告跟踪。

搜索广告的下载归因是以尊重隐私的方式完成的。一旦一个新增客户打开您的应用后，您的应用会查询客户的设备，以确定下载是否可归因于搜索广告：

* 查询完全在设备上进行;
* 您只能对应用的当前客户执行查询; 并且
* 用户可以启用限制广告跟踪功能来阻止查询。