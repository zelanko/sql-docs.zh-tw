---
title: "SQL Server 2016 版本資訊 | Microsoft Docs"
ms.date: 02/27/2018
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: sql-non-specified
ms.reviewer: 
ms.suite: sql
ms.custom: 
ms.technology:
- server-general
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- build notes
- release issues
ms.assetid: c64077a2-bec8-4c87-9def-3dbfb1ea1fb6
caps.latest.revision: 
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 6485ef83b940ab9d04b9406e461517d5254aec7f
ms.sourcegitcommit: 1a3584a60c12521ba5b4b12a18d8cb32b1f2d555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/28/2018
---
# <a name="sql-server-2016-release-notes"></a>SQL Server 2016 版本資訊
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]
本文說明 SQL Server 2016 版的限制和問題。 如需新功能的相關資訊，請參閱 [SQL Server 2016 的新功能](https://docs.microsoft.com/en-us/sql/sql-server/what-s-new-in-sql-server-2016)。

> [![Download from Evaluation Center](../includes/media/download2.png)](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016)  Download SQL Server 2016  from the **[Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016)**
>
> [![Azure 虛擬機器小型](../includes/media/azure-vm.png)](https://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2016sp1standardwindowsserver2016/) 擁有 Azure 帳戶嗎？  接著前往 **[這裡](https://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2016sp1standardwindowsserver2016/)** 來啟動已安裝 SQL Server 2016 SP1 的虛擬機器。
>
> [![下載 SSMS](../includes/media/download2.png)](../ssms/download-sql-server-management-studio-ssms.md) 如要取得最新版的 SQL Server Management Studio，請參閱**[下載 SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md)**。

## <a name="bkmk_2016sp1"></a>SQL Server 2016 Service Pack 1 (SP1) 可供使用
![info_tip](../sql-server/media/info-tip.png) SQL Server 2016 SP1 會將 SQL Server 2016 的所有版本和服務層級升級到 SQL Server 2016 SP1。 除了本文所列的修正程式，SQL Server 2016 SP1 還會提供 SQL Server 2016 累積更新 1 (CU1) 至 SQL Server 2016 CU3 中所包含的 Hotfix。

- [SQL Server 2016 SP1 下載頁面](https://www.microsoft.com/download/details.aspx?id=54276)
- [SQL Server 2016 Service Pack 1 版本資訊](https://support.microsoft.com/kb/3182545) 列出個別的 bug 編號，以及 SP1 中已修正或變更的問題。
 - ![info_tip](../sql-server/media/info-tip.png) 請參閱 [SQL Server 更新中心](https://msdn.microsoft.com/library/ff803383.aspx)，以取得所有支援版本的連結和資訊，包括下列項目的 Service Pack： [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 

##  <a name="bkmk_2016_ga"></a> SQL Server 2016 Release - General Availability (GA)
-   [Database Engine (GA)](#bkmk_ga_instalpatch) 
-   [Stretch Database (GA)](#bkmk_ga_stretch)
-   [查詢存放區 (GA)](#bkmk_ga_query_store)
-   [產品文件 (GA)](#bkmk_ga_docs)
 
### ![repl_icon_warn](../database-engine/availability-groups/windows/media/repl-icon-warn.gif) <a name="bkmk_ga_instalpatch"></a> Install Patch Requirement (GA) 
Microsoft 發現影響 Microsoft VC++ 2013 Runtime 二進位檔的問題，SQL Server 2016 必須安裝這些二進位檔。 已提供修正此問題的更新。 如果不安裝 VC Runtime 二進位檔的這項更新，SQL Server 2016 就可能在特定情況下遇到穩定性問題。 安裝 SQL Server 2016 之前，請先檢查電腦是否需要 [KB 3164398](http://support.microsoft.com/kb/3164398)中所述的填補。 修補程式也包含在 [SQL Server 2016 RTM 的累計更新套件 1 (CU1)](https://www.microsoft.com/download/details.aspx?id=53338)。 

**解決方式：**請使用下列其中一種解決方案：

- 安裝 [KB 3138367 - Visual C++ 2013 年和 Visual C++ 的可轉散發套件的更新](http://support.microsoft.com/kb/3138367)。 此 KB 是慣用的解決方式。 您可以在安裝 SQL Server 2016 之前或之後安裝此更新。 

    如已安裝 SQL Server 2016，請依序執行下列步驟︰

    1.  下載適當的 *vcredist_\*exe*。
    1.  停止資料庫引擎所有執行個體的 SQL Server 服務。
    1.  安裝 **KB 3138367**。
    1.  重新啟動電腦。
 

 - 安裝  [KB 3164398 - SQL Server 2016 MSVCRT 必要條件的重大更新](http://support.microsoft.com/kb/3164398)。  
 
    如果使用 **KB 3164398**，就可以在 SQL Server 安裝期間，透過 Microsoft Update 或從 Microsoft 下載中心安裝。 

    - **在 SQL Server 2016 安裝期間︰**如果執行 SQL Server 安裝程式的電腦可以存取網際網路，SQL Server 安裝程式會檢查更新是否為完整 SQL Server 安裝的一部分。 如果您接受更新，安裝程式會在安裝期間下載並更新二進位檔案。

    - **Microsoft Update：** Microsoft Update 現提供更新作為重要的非安全性 SQL Server 2016 更新。 透過 Microsoft Update 安裝，SQL Server 2016 會在更新後要求重新啟動伺服器。 

    - **下載中心：** 最後，Microsoft 下載中心會提供更新。 您可以下載更新的軟體，將它安裝在有 SQL Server 2016 的伺服器上。 


### <a name="bkmk_ga_stretch"></a>Stretch Database

#### <a name="problem-with-a-specific-character-in-a-database-or-table-name"></a>資料庫或資料表名稱中的特定字元問題

**問題和客戶影響：**嘗試在資料庫或資料表上啟用 Stretch Database 會失敗，並發生錯誤。 如果物件的名稱包含從小寫轉換為大寫時視為不同字元的字元，則會發生此問題。 導致此問題的字元範例是字元 "ƒ" (鍵入 ALT+159 所建立)。

**因應措施︰** 如果您想要啟用資料庫或資料表的 Stretch Database，重新命名物件並移除問題字元，是唯一的選項。

#### <a name="problem-with-an-index-that-uses-the-include-keyword"></a>使用 INCLUDE 關鍵字的索引問題

**問題和對客戶的影響︰** 如果資料表的索引使用 INCLUDE 關鍵字在索引中包含其他資料行，則嘗試啟用此資料表的 Stretch Database 會因發生錯誤而失敗。

**因應措施︰** 卸除使用 INCLUDE 關鍵字的索引，啟用資料表的 Stretch Database，然後重新建立索引。 如果這樣做，請務必依照貴組織的維護作法和原則，以確保對受影響資料表的使用者造成最小的影響或不受影響。

### <a name="bkmk_ga_query_store"></a>Query Store

#### <a name="problem-with-automatic-data-cleanup-on-editions-other-than-enterprise-and-developer"></a>Enterprise 和 Developer 以外版本的自動資料清除問題

 **問題和對客戶的影響：** Enterprise 和 Developer 以外版本的自動資料清除會失敗。 因此，如果不手動清除資料，查詢存放區所使用的空間會與日俱增，直到達到設定的限制。 如果不降低，此問題也會填滿為錯誤記錄檔配置的磁碟空間，因為每次嘗試執行清除都會產生傾印檔案。 啟動清除的期間長短取決於工作負載的頻率，但不超過 15 分鐘。

 **因應措施︰** 如果您打算在 Enterprise 和 Developer 以外的版本上使用查詢存放區，您必須明確關閉清除原則。 它可以從 SQL Server Management Studio ([資料庫屬性] 頁面)，或透過 TRANSACT-SQL 指令碼完成︰

```ALTER DATABASE <database name> SET QUERY_STORE (OPERATION_MODE = READ_WRITE, CLEANUP_POLICY = (STALE_QUERY_THRESHOLD_DAYS = 0), SIZE_BASED_CLEANUP_MODE = OFF)```

此外，請考慮手動清除選項，以防止查詢存放區轉換為唯讀模式。 例如，執行下列查詢，定期清理整個資料空間︰

```ALTER DATABASE <database name> SET QUERY_STORE CLEAR```

亦請執行下列查詢存放區預存程序，定期清理執行階段統計資料、特定的查詢或計劃︰

- `sp_query_store_reset_exec_stats`

- `sp_query_store_remove_plan`

- `sp_query_store_remove_query`


###  <a name="bkmk_ga_docs"></a> 產品文件 (GA) 
 **問題和客戶的影響：** SQL Server 2016 文件的可下載版本尚未提供。 當您嘗試使用 Help Library 管理員 **從線上安裝內容**時，您會看到 SQL Server 2012 及 SQL Server 2014 文件，但沒有 SQL Server 2016 文件的選項。    
    
 **因應措施：**使用下列其中一項因應措施：    
    
 ![管理適用於 SQL Server 的說明設定](../sql-server/media/docs-sql2016-managehelpsettings.png "管理適用於 SQL Server 的說明設定")    
    
-   使用選項 [選擇線上或本機說明]  ，並設定「我想要使用線上說明」的說明。    
    
-   使用選項 [從線上安裝內容]  ，並下載 SQL Server 2014 內容。    
    
 **F1 說明︰**依設計，當您在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中按下 F1 時，瀏覽器即會顯示 F1 說明文章的線上版本。 此問題是以瀏覽器為基礎的說明，即使您已設定並安裝本機說明也是一樣。 
     
**更新內容︰**    
在 SQL Server Management Studio 和 Visual Studio 中，加入文件程序期間可能會凍結 (擱置) 說明檢視器應用程式。 若要解決此問題，請完成下列步驟。 如需此問題的詳細資訊，請參閱 [Visual Studio 說明檢視器凍結在啟動顯示畫面上](https://msdn.microsoft.com/library/mt654096.aspx)。    
    
* 以 [記事本] 開啟 %LOCALAPPDATA%\Microsoft\HelpViewer2.2\HlpViewer_SSMS16_en-US.settings | HlpViewer_VisualStudio14_en-US.settings 檔案，將下列程式碼中的日期變更為未來的日期。    
    
     
```    
     Cache LastRefreshed="12/31/2017 00:00:00"    
``` 

## <a name="additional-information"></a>其他資訊
+ [SQL Server 2016 安裝](../database-engine/install-windows/installation-for-sql-server-2016.md)
+ [SQL Server 更新中心 - 所有已支援版本的連結和資訊](https://msdn.microsoft.com/library/ff803383.aspx)


[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]    

![MS_Logo_X-Small](../sql-server/media/ms-logo-x-small.png "MS_Logo_X-Small")    
