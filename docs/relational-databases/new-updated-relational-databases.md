---
title: "已更新 - 關聯式資料庫文件 | Microsoft Docs"
description: "針對關聯式資料庫，顯示文件最新變更之已更新內容的程式碼片段。"
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: BYHAM
ms.service: na
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.workload: relational-databases
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 09/11/2017
ms.author: genemi
ms.translationtype: HT
ms.sourcegitcommit: 15080827744c19120a8474f3142004c4af7a4064
ms.openlocfilehash: ee7d66bcd8720234f4aec97d24ce16ed21888a3c
ms.contentlocale: zh-tw
ms.lasthandoff: 09/13/2017

---
# <a name="new-and-recently-updated-relational-databases-docs"></a>新的與最近更新的文章： 關聯式資料庫文件



Microsoft 幾乎每天都會在其 [Docs.Microsoft.com](http://docs.microsoft.com/) 文件網站上更新一些現有文章。 本文會顯示最近更新文章的摘錄。 可能也會列出新文章的連結。

本文是透過定期重新執行的程式所產生。 摘錄中偶爾會出現示不完整的格式，或顯示為來自來源文章的 Markdown。 影像永遠不會顯示在這裡。

新的更新會報告下列日期範圍和主旨：



- *更新日期範圍：* &nbsp; **2017 年 7 月 18 日** &nbsp; -至- &nbsp; **2017 年 9 月 11 日**
- *主旨區域：* &nbsp; **關聯式資料庫**。




&nbsp;

## <a name="new-articles-created-recently"></a>最近建立的新文章

下列連結會跳至最近新增的新文章。


1. [將 Excel 中的資料匯入 SQL Server 或 Azure SQL Database](import-export/import-data-from-excel-to-sql.md)
2. [對 PolyBase Kerberos 的連線問題進行疑難排解](polybase/polybase-troubleshoot-connectivity.md)
3. [透明資料加密 (TDE)](security/encryption/transparent-data-encryption.md)
4. [Azure SQL Database 和資料倉儲的透明資料加密](security/encryption/transparent-data-encryption-azure-sql.md)
5. [Azure SQL Database 和資料倉儲的透明資料加密與攜帶您自己的金鑰支援](security/encryption/transparent-data-encryption-byok-azure-sql.md)
6. [PowerShell：使用您自己的 Azure Key Vault 金鑰來啟用透明資料加密](security/encryption/transparent-data-encryption-byok-azure-sql-configure.md)
7. [使用 PowerShell 輪替透明資料加密 (TDE) 保護裝置](security/encryption/transparent-data-encryption-byok-azure-sql-key-rotation.md)
8. [使用 PowerShell 移除透明資料加密 (TDE) 保護裝置](security/encryption/transparent-data-encryption-byok-azure-sql-remove-tde-protector.md)
9. [SQL Server 共用管理物件 (SMO) 授權條款](server-management-objects-smo/smo-license-terms.md)
10. [sys.external_libraries (Transact-SQL)](system-catalog-views/sys-external-libraries-transact-sql.md)
11. [sys.external_library_files (Transact-SQL)](system-catalog-views/sys-external-library-files-transact-sql.md)
12. [sp_rxPredict](system-stored-procedures/sp-rxpredict-transact-sql.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>更新文章與摘要

本節會顯示從最近發生大規模更新的文章所收集的更新摘錄。

此處顯示的摘錄不同於其適當語意內容。 此外，有時摘錄也與實際文件四周的重要 Markdown 語法不同。 因此，這些摘錄僅適用於一般指導方針。 摘錄只能讓您知道您感興趣的項目，是否值得花時間按一下並瀏覽實際文章。

由於這些和其他原因，請勿從這些摘錄中複製程式碼，而且不要將任何文字摘錄視為確切事實。 請改瀏覽實際文章。





&nbsp;

<a name="compactupdatedlist"/>

## <a name="compact-list-of-articles-updated-recently"></a>最近更新文章的壓縮清單

此壓縮清單提供所有更新文章的連結，並將列於＜摘要＞一節。

1. [自動調整](#TitleNum_1)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-automatic-tuningautomatic-tuningautomatic-tuningmd"></a>1.&nbsp; [自動調整](automatic-tuning/automatic-tuning.md)

*更新日期：2017 年 8 月 16 日* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 

<!-- Source markdown line 64.  ms.author= "jovanpop".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 be765a1acf9bdfd5485520d16160677583e81f8e 135d926227094374e6ec5484e7babee625b44bb2  (PR=2860  ,  Filename=automatic-tuning.md  ,  Dirpath=docs\relational-databases\automatic-tuning\  ,  MergeCommitSha40=e4a6157cb56c6db911406585f841046a431eef99) -->



**自動計畫選擇更正**


..!NCLUDE-NotShown--ssde_md--../../includes/ssde_md.md)] 只要偵測到計畫選擇迴歸，就可以自動切換到最後一個已知的良好計畫。

![SQL plan choice correction--media/force-last-good-plan.png "SQL 計畫選擇更正")

..!NCLUDE-NotShown--ssde_md--../../includes/ssde_md.md)] 會自動偵測任何可能的計畫選擇迴歸，包括應該使用的計畫，而不是錯誤的計畫。
當 ..!NCLUDE-NotShown--ssde_md--../../includes/ssde_md.md)] 運用最後一個已知的計畫時，會自動監視強制計畫的效能。 如果強制執行的計畫不比迴歸的計畫好，則不會強制執行新的計畫，且 ..!NCLUDE-NotShown--ssde_md--../../includes/ssde_md.md)] 會編譯新的計畫。 如果 ..!NCLUDE-NotShown--ssde_md--../../includes/ssde_md.md)] 確認強制計畫比迴歸計畫好，則保留強制計畫直到重新編譯 (例如，下次統計資料或結構描述變更)，如果它比迴歸計畫好。

**啟用自動計畫選擇更正**


您可以依每個資料庫啟用自動調整，並指定只要偵測到某些計畫變更迴歸，就應該強制執行最後一個良好的計畫。 自動調整已使用下列命令啟用：

```
ALTER DATABASE current
SET AUTOMATIC_TUNING ( FORCE_LAST_GOOD_PLAN = ON );
```
一旦您開啟此選項，..!NCLUDE-NotShown--ssde_md--../../includes/ssde_md.md)] 就會自動強制執行估計的 CPU 增量高於 10 秒，或新計畫錯誤數目高於建議計畫錯誤數目的任何建議，並確認強制執行的計畫比目前的計畫更好。

**其他選項 - 手動計畫選擇更正**


沒有自動調整，使用者必須定期監視系統，並尋找迴歸的查詢。 如有任何計畫迴歸，使用者應該會發現一些。







## <a name="similar-articles"></a>類似的文章

<!--  HOW TO:
    Refresh this file's line items with the latest 'Count-in-Similars*' content.
    Then run Run-533-*.BAT
-->

本節會在公開的 GitHub 存放庫中，列出與其他主題區中最近更新的文章十分相似的文章：[MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/)。

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>具有新文章或最近更新文章的主題區

- [新文章 + 更新文章 (3+12)：**SQL 進階分析**文件](../advanced-analytics/new-updated-advanced-analytics.md)
- [新文章 + 更新文章 (5+0)：**連線到 SQL** 文件](../connect/new-updated-connect.md)
- [新文章 + 更新文章 (5+1)：**SQL 資料庫引擎**文件](../database-engine/new-updated-database-engine.md)
- [新文章 + 更新文章 (19+82)：**SQL Integration Services** 文件](../integration-services/new-updated-integration-services.md)
- [新文章 + 更新文章 (1+8)：**Linux for SQL** 文件](../linux/new-updated-linux.md)
- [新文章 + 更新文章 (12+1)：**SQL 關聯式資料庫**文件](../relational-databases/new-updated-relational-databases.md)
- [新文章 + 更新文章 (0+1)：**SQL Reporting Services** 文件](../reporting-services/new-updated-reporting-services.md)
- [新文章 + 更新文章 (7+1)：**Microsoft SQL Server** 文件](../sql-server/new-updated-sql-server.md)
- [新文章 + 更新文章 (1+1)：**SQL Server Data Tools (SSDT)** 文件](../ssdt/new-updated-ssdt.md)
- [新文章 + 更新文章 (0+2)：**SQL Server 移轉小幫手 (SSMA)** 文件](../ssma/new-updated-ssma.md)
- [新文章 + 更新文章 (1+4)：**SQL Server Management Studio (SSMS)** 文件](../ssms/new-updated-ssms.md)
- [新文章 + 更新文章 (4+1)：**Transact-SQL** 文件](../t-sql/new-updated-t-sql.md)
- [新文章 + 更新文章 (0+1)：**SQL 工具**文件](../tools/new-updated-tools.md)

#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>沒有新文章或最近更新文章的主題區

- [新文章 + 更新文章 (0+0)：**ActiveX Data Objects (ADO) for SQL** 文件](../ado/new-updated-ado.md)
- [新文章 + 更新文章 (0+0)：**SQL Analysis Services** 文件](../analysis-services/new-updated-analysis-services.md)
- [新文章 + 更新文章 (0+0)：**Data Quality Services for SQL** 文件](../data-quality-services/new-updated-data-quality-services.md)
- [新文章 + 更新文章 (0+0)：**SQL 資料採礦延伸模組 (DMX)** 文件](../dmx/new-updated-dmx.md)
- [新文章 + 更新文章 (0+0)：**SQL Master Data Services (MDS)** 文件](../master-data-services/new-updated-master-data-services.md)
- [新文章 + 更新文章 (0+0)：**SQL 多維度運算式 (MDX)** 文件](../mdx/new-updated-mdx.md)
- [新文章 + 更新文章 (0+0)：**SQL ODBC (開放式資料庫連接)** 文件](../odbc/new-updated-odbc.md)
- [新文章 + 更新文章 (0+0)：**PowerShell for SQL** 文件](../powershell/new-updated-powershell.md)
- [新文章 + 更新文章 (0+0)：**SQL 範例**文件](../sample/new-updated-sample.md)
- [新文章 + 更新文章 (0+0)：**XQuery for SQL** 文件](../xquery/new-updated-xquery.md)



