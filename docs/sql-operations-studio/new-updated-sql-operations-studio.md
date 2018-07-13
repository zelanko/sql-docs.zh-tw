---
title: 已更新-SQL Operations Studio 文件 |Microsoft 文件
description: 針對 SQL Operations Studio，顯示文件中最近變更的更新內容程式碼片段。
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.technology: release-landing
ms.prod: sql
ms.prod_service: sql-non-specified
ms.component: ssops
ms.date: 04/28/2018
ms.openlocfilehash: 074ed6176480655d9d87a55eb87cbb76b3011b7e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="new-and-recently-updated-sql-operations-studio-docs"></a>新增的與最近的更新： SQL Operations Studio 文件



幾乎每日 Microsoft 某些現有發行項上更新其[Docs.Microsoft.com](http://docs.microsoft.com/)文件網站。 這篇文章會顯示從最近已更新的發行項的摘錄。 可能也會列出新的文章連結。

這篇文章會定期重新執行程式所產生的。 偶爾摘錄會顯示具有完美的格式，或 markdown 從來源文件。 影像永遠不會顯示在這裡。

新的更新會報告下列日期範圍和主體：



- *日期範圍的更新：* &nbsp; **2018-02-03** &nbsp; -到- &nbsp; **2018-04-28**
- *主旨區域：* &nbsp; **SQL Operations Studio**。




&nbsp;

## <a name="new-articles-created-recently"></a>最近才建立新的發行項

下列連結會跳至最近新增的新文章。


- [擴充 SQL Operations Studio (預覽) 的功能](extensions.md)

<!-- GeneMi:  I MANUALLY replace the ugly !INCLUDE with the name from inside the includes file. -->


&nbsp;

## <a name="updated-articles-with-excerpts"></a>更新的發行項、 只有摘要

本節會顯示從最近發生大規模更新的文章所收集的更新摘錄。

此處顯示的摘錄顯示分隔其適當語意的內容。 此外，有時摘錄分開四周實際文件中的重要的 markdown 語法。 因此，這些摘錄適用於一般指導方針。 摘錄只會讓您知道您的興趣是否值得花時間按一下，瀏覽實際的發行項。

如需這些和其他原因，不要複製程式碼從這些摘錄中，而且不採用確切真為任何文字摘錄。 相反地，請瀏覽實際的發行項。





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>Compact 文件最近才更新清單

此壓縮清單提供＜摘要＞一節中所有更新文章的連結。

1. [下載並安裝 SQL Operations Studio （預覽）](#TitleNum_1)
2. [SQL Operations Studio （預覽） 版本資訊](#TitleNum_2)
3. [教學課程： 將*5 名最慢的查詢*範例資料庫儀表板的小工具](#TitleNum_3)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-download-and-install-sql-operations-studio-previewdownloadmd"></a>1.&nbsp; [下載並安裝 SQL Operations Studio （預覽）](download.md)

*更新日期︰ 2018-04-25* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([下一步](#TitleNum_2))

<!-- Source markdown line 64.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 6b4f80ad54c599e4354303a736f62e9715f99a32 18b22f464bbd8676348248ba5717b71acbab1c0d  (PR=5676  ,  Filename=download.md  ,  Dirpath=docs\sql-operations-studio\  ,  MergeCommitSha40=a85a46312acf8b5a59a8a900310cf088369c4150) -->



   **Debian 安裝：**
```
   cd ~
   sudo dpkg -i ./Downloads/sqlops-linux-<version string>.deb

   sqlops
```

   **rpm 安裝：**
```
   cd ~
   yum install ./Downloads/sqlops-linux-<version string>.rpm

   sqlops
```

   **.tar.gz 安裝：**



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-sql-operations-studio-preview-release-notesrelease-notesmd"></a>2.&nbsp; [SQL Operations Studio （預覽） 版本資訊](release-notes.md)

*更新日期︰ 2018-04-25* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([先前](#TitleNum_1) | [下一步](#TitleNum_3))

<!-- Source markdown line 20.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 e2901d8a197f375f7d10ec93cbc9320362bf9278 0dde1aceceb339cb4cacd744e469f3d85d589668  (PR=5676  ,  Filename=release-notes.md  ,  Dirpath=docs\sql-operations-studio\  ,  MergeCommitSha40=a85a46312acf8b5a59a8a900310cf088369c4150) -->



**[下載 4 月公開預覽]**


**2018 年 4 月  （4 月公開預覽）**


發行日期： 2018 年 4 月 25 日，版本： 0.28.6

*4 月公開預覽版*包含 bug 修正和增強功能。

- SQL 代理程式預覽擴充功能的增強功能。
- 針對在 SQL Operations Studio 內儲存受系統管理保護與大於 256M 的檔案，改善大型和受保護檔案的支援。
- 若要同時使用多個開啟的終端機分割整合式的終端機。
- 降低的安裝磁碟上檔案計數呎列印更快的安裝和啟動時間。
- 繼續以修正 GitHub 問題：
   - 修正[發出 37](https://github.com/Microsoft/sqlopsstudio/issues/37)： 當圖表檢視器擲回錯誤時，就會發生未預期的行為。
   - 修正[發出 462](https://github.com/Microsoft/sqlopsstudio/issues/462)： 功能要求： 根據預設展開伺服器群組的選項。
   - 修正[發出 606](https://github.com/Microsoft/sqlopsstudio/issues/606): intellisense-'update' 命令的錯誤提供建議。
   - 修正[發出 967](https://github.com/Microsoft/sqlopsstudio/issues/967)： 預期的查詢計劃當結果方格中選取 XML 顯示計畫。
   - 修正[發出 1023年](https://github.com/Microsoft/sqlopsstudio/issues/1023)： 從 flyfishingdba 新增 ms_foreachdb 呼叫的方括號。
   - 修正[發出 1048年](https://github.com/Microsoft/sqlopsstudio/issues/1048)： 登入前 SSL/TLS 信號交換時發生錯誤。
   - 修正[發出 1050年](https://github.com/Microsoft/sqlopsstudio/issues/1050)： 清除 insights 檢視之前顯示錯誤。
   - 修正[發出 1057年](https://github.com/Microsoft/sqlopsstudio/issues/1057)： 還原和檔案總管 widget 中的新查詢動作已中斷。



&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-tutorial-add-the-five-slowest-queries-sample-widget-to-the-database-dashboardtutorial-qds-sql-servermd"></a>3.&nbsp; [教學課程： 將*5 名最慢的查詢*範例資料庫儀表板的小工具](tutorial-qds-sql-server.md)

*更新日期︰ 2018-04-25* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([先前](#TitleNum_2))

<!-- Source markdown line 94.  ms.author= "erickang".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 bc128acd966898cafc04381d7d83187d28466052 a47bf93ea4165618e0e514d7900ce1461f691aae  (PR=5676  ,  Filename=tutorial-qds-sql-server.md  ,  Dirpath=docs\sql-operations-studio\  ,  MergeCommitSha40=a85a46312acf8b5a59a8a900310cf088369c4150) -->



       },
       {
           "name": "Tasks",
           "gridItemConfig": {
               "sizex": 1,
               "sizey": 1
           },
           "widget": {
               "tasks-widget": {}
           }
       },
       {
           "gridItemConfig": {
               "sizex": 1,
               "sizey": 2
           },
           "widget": {
               "explorer-widget": {}
           }







## <a name="similar-articles-about-new-or-updated-articles"></a>新文章或更新文章的類似文章

本節會在我們的公開 GitHub 存放庫中，列出與其他主題區中最近更新的文章十分相似的文章：[MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/)。



#### <a name="subject-areas-that-do-have-new-or-recently-updated-articles"></a>具有新文章或最近更新文章的主題區

- [新增 + 更新 (11 + 6): &nbsp; &nbsp; **Advanced Analytics sql**文件](../advanced-analytics/new-updated-advanced-analytics.md)
- [新增 + 更新 (18 + 0): &nbsp; &nbsp; **sql Analysis Services**文件](../analysis-services/new-updated-analysis-services.md)
- [新增 + 更新 (218 + 14):**連接到 SQL**文件](../connect/new-updated-connect.md)
- [新增 + 更新 (14 + 0): &nbsp; &nbsp; **sql 資料庫引擎**文件](../database-engine/new-updated-database-engine.md)
- [新增 + 更新 (3 + 2): &nbsp; &nbsp; **sql Integration Services**文件](../integration-services/new-updated-integration-services.md)
- [新增 + 更新 (3 + 3): &nbsp; &nbsp; **sql Linux**文件](../linux/new-updated-linux.md)
- [新增 + 更新 (7 + 10): &nbsp; &nbsp;**關聯式資料庫供 SQL**文件](../relational-databases/new-updated-relational-databases.md)
- [新增 + 更新 (0 + 2): &nbsp; &nbsp; **Reporting Services SQL**文件](../reporting-services/new-updated-reporting-services.md)
- [新增 + 更新 (1 + 3): &nbsp; &nbsp; **SQL Operations Studio**文件](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [新增 + 更新 (2 + 3): &nbsp; &nbsp; **Microsoft SQL Server**文件](../sql-server/new-updated-sql-server.md)
- [新增 + 更新 (1 + 1): &nbsp; &nbsp; **SQL Server Data Tools (SSDT)** 文件](../ssdt/new-updated-ssdt.md)
- [新增 + 更新 (5 + 2): &nbsp; &nbsp; **SQL Server Management Studio (SSMS)** 文件](../ssms/new-updated-ssms.md)
- [新增 + 更新 (0 + 2): &nbsp; &nbsp; **TRANSACT-SQL**文件](../t-sql/new-updated-t-sql.md)
- [新增 + 更新 (1 + 1): &nbsp; &nbsp; **Tools for SQL**文件](../tools/new-updated-tools.md)



#### <a name="subject-areas-that-do-not-have-any-new-or-recently-updated-articles"></a>沒有新文章或最近更新文章的主題區

- [新增 + 更新 (0 + 0): **Analytics Platform System sql**文件](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [新增 + 更新 (0 + 0): **SQL 的 Data Quality Services**文件](../data-quality-services/new-updated-data-quality-services.md)
- [新增 + 更新 (0 + 0):**資料採礦延伸模組 (DMX)，sql**文件](../dmx/new-updated-dmx.md)
- [新文章 + 更新文章 (0+0)：**SQL Master Data Services (MDS)** 文件](../master-data-services/new-updated-master-data-services.md)
- [新增 + 更新 (0 + 0)：**適用於 SQL 的多維度運算式 (MDX)** 文件](../mdx/new-updated-mdx.md)
- [新增 + 更新 (0 + 0)：**ODBC (開放式資料庫連接) for SQL** 文件](../odbc/new-updated-odbc.md)
- [新增 + 更新 (0 + 0)：**適用於 SQL 的 PowerShell** 文件](../powershell/new-updated-powershell.md)
- [新增 + 更新 (0 + 0):**範例 sql**文件](../samples/new-updated-samples.md)
- [新增 + 更新 (0 + 0): **SQL Server 移轉小幫手 (SSMA)** 文件](../ssma/new-updated-ssma.md)
- [新增 + 更新 (0 + 0): **sql XQuery**文件](../xquery/new-updated-xquery.md)

