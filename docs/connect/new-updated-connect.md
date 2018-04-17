---
title: 已更新-連接到 SQL Server 文件 |Microsoft 文件
description: 顯示更新的內容，如需連接到 Microsoft SQL Server 中最近變更過的文件的程式碼片段。
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.prod_service: sql-non-specified
ms.component: connect
ms.date: 02/03/2018
ms.openlocfilehash: da7ff58d5930acb084220c8d0364147ae93ed963
ms.sourcegitcommit: d6b1695c8cbc70279b7d85ec4dfb66a4271cdb10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2018
---
# <a name="new-and-recently-updated-connect-to-sql-server"></a>新增和更新最近： 連接到 SQL Server



幾乎每日 Microsoft 某些現有發行項上更新其[Docs.Microsoft.com](http://docs.microsoft.com/)文件網站。 這篇文章會顯示從最近已更新的發行項的摘錄。 可能也會列出新的文章連結。

這篇文章會定期重新執行程式所產生的。 偶爾摘錄會顯示具有完美的格式，或 markdown 從來源文件。 影像永遠不會顯示在這裡。

新的更新會報告下列日期範圍和主體：



- 更新日期範圍：&nbsp;**2017 年 12 月 3 日**&nbsp;-至-&nbsp;**2018 年 2 月 3 日**
- *主旨區域：* &nbsp; **連接到 SQL Server**。




&nbsp;

## <a name="new-articles-created-recently"></a>最近才建立新的發行項

下列連結會跳至最近新增的新文章。


***目前無新文章列出。***



&nbsp;

## <a name="updated-articles-with-excerpts"></a>更新的發行項、 只有摘要

本節會顯示從最近發生大規模更新的文章所收集的更新摘錄。

此處顯示的摘錄顯示分隔其適當語意的內容。 此外，有時摘錄分開四周實際文件中的重要的 markdown 語法。 因此，這些摘錄適用於一般指導方針。 摘錄只會讓您知道您的興趣是否值得花時間按一下，瀏覽實際的發行項。

如需這些和其他原因，不要複製程式碼從這些摘錄中，而且不採用確切真為任何文字摘錄。 相反地，請瀏覽實際的發行項。





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>Compact 文件最近才更新清單

此壓縮清單提供＜摘要＞一節中所有更新文章的連結。

1. [搭配使用一律加密 with the ODBC Driver for SQL Server](#TitleNum_1)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-using-always-encrypted-with-the-odbc-driver-for-sql-serverodbcusing-always-encrypted-with-the-odbc-drivermd"></a>1.&nbsp; [搭配使用一律加密 with the ODBC Driver for SQL Server](odbc/using-always-encrypted-with-the-odbc-driver.md)

*更新日期︰ 2018年-01-22* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 

<!-- Source markdown line 524.  ms.author= "v-chojas".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 a52abae2a8f27c3b5bc411ef758610116a608f9f 352368eb269b98ab5ca3a9791fae2e70bf26277a  (PR=4686  ,  Filename=using-always-encrypted-with-the-odbc-driver.md  ,  Dirpath=docs\connect\odbc\  ,  MergeCommitSha40=82c9868b5bf95e5b0c68137ba434ddd37fc61072) -->



**在使用 SQLGetData 組件中擷取資料**

SQL server ODBC 驅動程式 17 加密之前使用 SQLGetData 組件中無法擷取字元和二進位資料行。 可以進行只有一個呼叫 SQLGetData，以包含整個資料行的資料長度足夠的緩衝區。

**將資料傳送 SQLPutData 使用組件中**

插入或比較資料無法傳送 SQLPutData 使用組件中。 可以進行 SQLPutData 只有一個呼叫，以包含整個資料緩衝區。 Long 資料插入加密的資料行中，使用下一節中所述，與輸入的資料檔大量複製 API。

**加密的 money 和 smallmoney**

加密**money**或**smallmoney**資料行不能為目標的參數，因為沒有任何特定 ODBC 資料類型並對應至這些型別，造成運算元類型衝突錯誤。

**大量複製加密的資料行**


使用[SQL 大量複製函數](odbc/../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)和**bcp**公用程式使用 永遠加密後 ODBC 驅動程式 17 for SQL Server 支援。 純文字 （插入上加密和解密上擷取） 和加密文字 （逐字傳輸） 可插入和擷取使用大量複製 （bcp_ *） 應用程式開發介面和**bcp**公用程式。

- 要擷取密碼文字形式 （例如，用於大量載入不同的資料庫） varbinary （max）、 連接，而不`ColumnEncryption`選項 (或將它設定為`Disabled`) 和執行 BCP OUT 作業。

- 插入和擷取純文字，並讓此驅動程式會明確地執行加密和解密為必要項目，設定`ColumnEncryption`至`Enabled`已足夠。 BCP API 的功能則未變更。

- 若要在 varbinary （max） 的形式 （例如上方處擷取） 插入加密文字，請設定`BCPMODIFYENCRYPTED`選項設定為 TRUE，並執行 BCP IN 作業。 為了讓未產生資料，請確認目的地資料行的 CEK 是原先取得從中加密文字相同。







## <a name="similar-articles-about-new-or-updated-articles"></a>新文章或更新文章的類似文章

本節會在我們的公開 GitHub 存放庫中，列出與其他主題區中最近更新的文章十分相似的文章：[MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/)。


#### <a name="subject-areas-that-do-have-new-or-recently-updated-articles"></a>具有新文章或最近更新文章的主題區


- [新文章 + 更新文章 (1+3)：&nbsp;**Advanced Analytics for SQL** 文件](../advanced-analytics/new-updated-advanced-analytics.md)
- [新文章 + 更新文章 (0+1)：&nbsp;**Analytics Platform System for SQL** 文件](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [新文章 + 更新文章 (0+1)：&nbsp;**連線到 SQL** 文件](../connect/new-updated-connect.md)
- [新文章 + 更新文章 (0+1)：&nbsp;**Database Engine for SQL** 文件](../database-engine/new-updated-database-engine.md)
- [新文章 + 更新文章 (12+1)：**Integration Services for SQL**  文件](../integration-services/new-updated-integration-services.md)
- [新文章 + 更新文章 (6+2)：&nbsp;**Linux for SQL** 文件](../linux/new-updated-linux.md)
- [新文章 + 更新文章 (15+0)：**PowerShell for SQL** 文件](../powershell/new-updated-powershell.md)
- [新文章 + 更新文章 (2+9)：&nbsp;**Relational Databases for SQL** 文件](../relational-databases/new-updated-relational-databases.md)
- [新文章 + 更新文章 (1+0)：&nbsp;**Reporting Services for SQL** 文件](../reporting-services/new-updated-reporting-services.md)
- [新文章 + 更新文章 (1+1)：&nbsp;**SQL Operations Studio** 文件](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [新文章 + 更新文章 (1+1)：&nbsp;**Microsoft SQL Server** 文件](../sql-server/new-updated-sql-server.md)
- [新文章 + 更新文章 (0+1)：&nbsp;**SQL Server Data Tools (SSDT)** 文件](../ssdt/new-updated-ssdt.md)
- [新文章 + 更新文章 (1+2)：&nbsp;**SQL Server Management Studio (SSMS)** 文件](../ssms/new-updated-ssms.md)
- [新文章 + 更新文章 (0+2)：&nbsp;**Transact-SQL** 文件](../t-sql/new-updated-t-sql.md)



#### <a name="subject-areas-that-do-not-have-any-new-or-recently-updated-articles"></a>沒有新文章或最近更新文章的主題區


- [新文章 + 更新文章 (0+0)：**SQL 資料移轉小幫手 (DMA)** 文件](../dma/new-updated-dma.md)
- [新 + 更新 (0 + 0): **ActiveX Data Objects (ADO) 的 SQL**文件](../ado/new-updated-ado.md)
- [新文章 + 更新文章 (0+0)：**SQL Analysis Services** 文件](../analysis-services/new-updated-analysis-services.md)
- [新 + 更新 (0 + 0): **SQL 的 Data Quality Services**文件](../data-quality-services/new-updated-data-quality-services.md)
- [新 + 更新 (0 + 0):**資料採礦延伸模組 (DMX)，sql**文件](../dmx/new-updated-dmx.md)
- [新文章 + 更新文章 (0+0)：**SQL Master Data Services (MDS)** 文件](../master-data-services/new-updated-master-data-services.md)
- [新 + 更新 (0 + 0):**多維度運算式 (MDX) 的 SQL**文件](../mdx/new-updated-mdx.md)
- [新 + 更新 (0 + 0): **ODBC （開放式資料庫連接） 的 SQL**文件](../odbc/new-updated-odbc.md)
- [新 + 更新 (0 + 0):**範例 sql**文件](../samples/new-updated-samples.md)
- [新 + 更新 (0 + 0): **SQL Server 移轉小幫手 (SSMA)**文件](../ssma/new-updated-ssma.md)
- [新文章 + 更新文章 (0+0)：**SQL 的工具** 文件](../tools/new-updated-tools.md)
- [新 + 更新 (0 + 0): **sql XQuery**文件](../xquery/new-updated-xquery.md)


