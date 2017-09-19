---
title: "已更新 - SSMS for SQL Server 文件 | Microsoft Docs"
description: "顯示最近變更過的文件更新內容，SQL Server Management Studio (SSMS) for Microsoft SQL Server 的程式碼片段。"
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
ms.service: na
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 09/11/2017
ms.author: genemi
ms.workload: ssms-sql-server-management-studio
ms.translationtype: HT
ms.sourcegitcommit: 15080827744c19120a8474f3142004c4af7a4064
ms.openlocfilehash: 917198902baf85f2bae57c9ade9f8d3e29dea357
ms.contentlocale: zh-tw
ms.lasthandoff: 09/13/2017

---
# <a name="new-and-recently-updated-sql-server-management-studio-ssms-for-sql-server"></a>新文章和最近更新的文章：SQL Server Management Studio (SSMS) for SQL Server



Microsoft 幾乎每天都會在其 [Docs.Microsoft.com](http://docs.microsoft.com/) 文件網站上更新一些現有文章。 本文會顯示最近更新文章的摘錄。 可能也會列出新文章的連結。

本文是透過定期重新執行的程式所產生。 摘錄中偶爾會出現示不完整的格式，或顯示為來自來源文章的 Markdown。 影像永遠不會顯示在這裡。

新的更新會報告下列日期範圍和主旨：



- *更新的日期範圍：* &nbsp;**2017-07-18** &nbsp; 到 &nbsp; **2017-09-11**
- *主題區：*&nbsp; **SQL Server Management Studio (SSMS)**。




&nbsp;

## <a name="new-articles-created-recently"></a>最近建立的新文章

下列連結會跳至最近新增的新文章。


1. [SQL Server Management Studio 中的輸出視窗](output-window.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>更新文章與摘要

本節會顯示從最近發生大規模更新的文章所收集的更新摘錄。

此處顯示的摘錄不同於其適當語意內容。 此外，有時摘錄也與實際文件四周的重要 Markdown 語法不同。 因此，這些摘錄僅適用於一般指導方針。 摘錄只能讓您知道您感興趣的項目，是否值得花時間按一下並瀏覽實際文章。

由於這些和其他原因，請勿從這些摘錄中複製程式碼，而且不要將任何文字摘錄視為確切事實。 請改瀏覽實際文章。





&nbsp;

<a name="compactupdatedlist"/>

## <a name="compact-list-of-articles-updated-recently"></a>最近更新文章的壓縮清單

此壓縮清單提供＜摘要＞一節中所有更新文章的連結。

1. [下載 SQL Server Management Studio (SSMS)](#TitleNum_1)
2. [連線至 SQL Server 或 Azure SQL Database](#TitleNum_2)
3. [SQL Server Management Studio - 變更記錄 (SSMS)](#TitleNum_3)
4. [建立及更新資料表](#TitleNum_4)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-download-sql-server-management-studio-ssmsdownload-sql-server-management-studio-ssmsmd"></a>1.&nbsp; [下載 SQL Server Management Studio (SSMS)](download-sql-server-management-studio-ssms.md)

*更新日期：2017-08-07* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([下一個](#TitleNum_2))

<!-- Source markdown line 63.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 23260f301f86651061b47065bee43d42c92a7be4 0c2178d96b621b96bfcd2fbb782f24792debb407  (PR=2775  ,  Filename=download-sql-server-management-studio-ssms.md  ,  Dirpath=docs\ssms\  ,  MergeCommitSha40=3f12671ace99d5fefc199c7b1c2db31e5b3cfade) -->



SSMS 17.2 是 SQL Server Management Studio 的最新版本。 17.x 世代的 SSMS 幾乎支援 SQL Server 2008 到 SQL Server 2017 的所有功能領域。 17.x 版也支援 SQL Analysis Service PaaS。

17.2 版包括：

- Multi-Factor Authentication (MFA)
  - 適用於具 Multi-Factor Authentication 的通用驗證 (具 MFA 的 UA) 的多使用者 Azure AD 驗證
  - 已針對具 MFA 的通用驗證新增使用者認證輸入欄位，以支援多使用者驗證。
- 連接對話方塊現在支援下列 5 種驗證方法：
  - Windows 驗證
  - SQL Server 驗證
  - Active Directory - 含 MFA 的通用支援
  - Active Directory - 密碼
  - Active Directory - 整合式

- DacFx 的資料庫匯入/匯出精靈現在可以使用具 MFA 的通用驗證。
- 如需 API 支援，請參閱 [IUniversalAuthProvider 介面](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.iuniversalauthprovider.aspx)。
- 具 MFA 的 Azure AD 通用驗證所使用的 ADAL Managed 程式庫已升級至 3.13.9 版。
- 新的 CLI 介面支援 SQL Database 和 SQL 資料倉儲的 Azure AD 管理員設定。

 如需 Active Directory 驗證方法的詳細資訊，請參閱 [SQL Database 和 SQL 資料倉儲的通用驗證 (MFA 的 SSMS 支援)](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication) 和[設定適用於 SQL Server Management Studio 的 Azure SQL Database Multi-Factor Authentication](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication-configure)。

- 輸出視窗包含在展開 [物件總管] 節點期間所執行查詢的項目
- Azure SQL Database 的已啟用檢視表設計工具
- SSMS 中從物件總管編寫物件指令碼的預設指令碼選項已變更：



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-connect-to-a-sql-server-or-azure-sql-databaseobjectconnect-to-an-instance-from-object-explorermd"></a>2.&nbsp; [連線至 SQL Server 或 Azure SQL Database](object/connect-to-an-instance-from-object-explorer.md)

*更新日期：2017-08-25* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([上一個](#TitleNum_1) | [下一個](#TitleNum_3))

<!-- Source markdown line 40.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 cfd72893c35c87df96dc8605807e542be28936e2 840981d3a115a15774a8e47ee2f6a0e5c4177b01  (PR=2961  ,  Filename=connect-to-an-instance-from-object-explorer.md  ,  Dirpath=docs\ssms\object\  ,  MergeCommitSha40=21f0cfd102a6fcc44dfc9151750f1b3c936aa053) -->



   ![firewall--../media/connect-to-server/new-firewall-rule.png)

1. 若要建立防火牆規則並連線至伺服器，請按一下 [確定]。

1. 成功連線後，伺服器會顯示在**物件總管**中：

   ![connected--../media/connect-to-server/connected.png)

**後續步驟**


[設計、建立及更新資料表--../visual-db-tools/design-tables-visual-database-tools.md)

**另請參閱**


[SQL Server Management Studio (SSMS)--../sql-server-management-studio-ssms.md) [下載 SQL Server Management Studio (SSMS)--../download-sql-server-management-studio-ssms.md)

[Analysis Services](https://docs.microsoft.com/sql/analysis-services/instances/connect-to-analysis-services)
[Integration Services](https://docs.microsoft.com/sql/integration-services/sql-server-integration-services)
[Reporting Services](https://docs.microsoft.com/sql/reporting-services/tools/connect-to-a-report-server-in-management-studio)



&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-sql-server-management-studio---changelog-ssmssql-server-management-studio-changelog-ssmsmd"></a>3.&nbsp; [SQL Server Management Studio - 變更記錄 (SSMS)](sql-server-management-studio-changelog-ssms.md)

*更新日期：2017-08-07* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([上一個](#TitleNum_2) | [下一個](#TitleNum_4))

<!-- Source markdown line 20.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 1733ce3c556db1e51cb27bf830429f2c42e8f97e 2abb24fd6547e438181039d095cbad027473a57e  (PR=2775  ,  Filename=sql-server-management-studio-changelog-ssms.md  ,  Dirpath=docs\ssms\  ,  MergeCommitSha40=3f12671ace99d5fefc199c7b1c2db31e5b3cfade) -->



本文提供目前版本和舊版本之 SSMS 的更新、改善和 Bug 修正詳細資料。 下載[下面的舊版 SSMS--#previous-ssms-releases)。

**[SSMS 17.2--download-sql-server-management-studio-ssms.md)**


正式運作 | 組建編號：14.0.17177.0

**增強功能**


- Multi-Factor Authentication (MFA)
  - 適用於具 Multi-Factor Authentication 的通用驗證 (具 MFA 的 UA) 的多使用者 Azure AD 驗證
  - 已針對具 MFA 的通用驗證新增使用者認證輸入欄位，以支援多使用者驗證。
- 連接對話方塊現在支援下列 5 種驗證方法：
  - Windows 驗證
  - SQL Server 驗證
  - Active Directory - 含 MFA 的通用支援
  - Active Directory - 密碼
  - Active Directory - 整合式

- DacFx 的資料庫匯入/匯出精靈現在可以使用具 MFA 的通用驗證。
- 如需 API 支援，請參閱 [IUniversalAuthProvider 介面](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.iuniversalauthprovider.aspx)。
- 具 MFA 的 Azure AD 通用驗證所使用的 ADAL Managed 程式庫已升級至 3.13.9 版。
- 此外，提供的新 CLI 介面可支援 SQL Database 和 SQL 資料倉儲的 Azure AD 管理員設定。

 如需 Active Directory 驗證方法的詳細資訊，請參閱 [SQL Database 和 SQL 資料倉儲的通用驗證 (MFA 的 SSMS 支援)](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication) 和[設定適用於 SQL Server Management Studio 的 Azure SQL Database Multi-Factor Authentication](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication-configure)。

- 輸出視窗包含在展開 [物件總管] 節點期間所執行查詢的項目



&nbsp;

&nbsp;

---

<a name="TitleNum_4"/>

### <a name="4-nbsp-create-and-update-database-tablesvisual-db-toolsdesign-tables-visual-database-toolsmd"></a>4.&nbsp; [建立及更新資料表](visual-db-tools/design-tables-visual-database-tools.md)

*更新日期：2017-08-25* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([上一個](#TitleNum_3))

<!-- Source markdown line 30.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 f63884ac2d04889e70c505cb5262c8dd81d73ee7 4b4c7aa5e8a0548405f02d11a66b722219fa78f0  (PR=2961  ,  Filename=design-tables-visual-database-tools.md  ,  Dirpath=docs\ssms\visual-db-tools\  ,  MergeCommitSha40=21f0cfd102a6fcc44dfc9151750f1b3c936aa053) -->



**建立資料表**


1. 以滑鼠右鍵按一下資料庫中的 [資料表] 節點，然後選取 [新增] > [資料表]：

    ![新增資料表--../media/design-tables/new-table.png)

1. 新增[資料行--column-properties-visual-database-tools.md)到您的資料表：

    ![設計資料表--../media/design-tables/new-table2.png)

1. 關閉設計工具並儲存變更。

**更新資料表**


1. 以滑鼠右鍵按一下資料庫中，[資料表] 節點下的資料表，然後選取 [設計]：

   ![更新資料表--../media/design-tables/update-table.png)

1. 更新想要的資料表設定：

   ![--../media/design-tables/update-table2.png)

1. 關閉設計工具並儲存變更。

**另請參閱**


[資料表](http://msdn.microsoft.com/82d7819c-b801-4309-a849-baa63083e83f) [資料表屬性 &#40;Visual Database Tools&#41;--../../ssms/visual-db-tools/table-properties-visual-database-tools.md) [資料行屬性--column-properties-visual-database-tools.md) [將資料行新增到資料表--../../relational-databases/tables/add-columns-to-a-table-database-engine.md) [主要與外部索引鍵--../../relational-databases/tables/primary-and-foreign-key-constraints.md) [索引--../../relational-databases/indexes/indexes.md) [資料類型 (Transact-SQL)--../../t-sql/data-types/data-types-transact-sql.md) [下載 SQL Server Management Studio (SSMS)--../download-sql-server-management-studio-ssms.md)







## <a name="similar-articles"></a>類似的文章

<!--  HOW TO:
    Refresh this file's line items with the latest 'Count-in-Similars*' content.
    Then run Run-533-*.BAT
-->

本節會在我們的公開 GitHub 存放庫中，列出與其他主題區中最近更新的文章十分相似的文章：[MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/)。

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



