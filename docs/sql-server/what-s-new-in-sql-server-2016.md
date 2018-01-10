---
title: "SQL Server 2016 的新功能"
ms.custom: 
ms.date: 07/21/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: sql-non-specified
ms.reviewer: 
ms.suite: sql
ms.technology: server-general
ms.tgt_pltfrm: 
ms.topic: article
keywords: "sql server 新功能"
helpviewer_keywords:
- new features [SQL Server]
- SQL Server, what's new
- SQL Server 2008 what's new
- what's new [SQL Server]
ms.assetid: 6a428023-e3cc-4626-a88a-4c13ccbd7db0
caps.latest.revision: "224"
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 075ad5ecefdef03acb8428cc199c35f6116c442b
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/09/2018
---
# <a name="whats-new-in-sql-server-2016"></a>SQL Server 2016 中的新功能
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]  
 使用 SQL Server 2016，您可以使用內建所有功能 (從記憶體內部效能和進階安全性到資料庫內分析) 的可調整混合式資料庫平台，建置智慧型的任務關鍵應用程式。 SQL Server 2016 版本新增了新的安全性功能、查詢能力、Hadoop 和雲端整合、R 分析等等，以及許多改進和增強功能。 

此頁面會提供摘要資訊，以及能針對每個 SQL Server 元件提供詳細資料的 SQL Server 2016 新功能資訊連結。 

![SQL Server 2016](../sql-server/media/sql-server-2016.png) 

 **立即試用 SQL Server！** 
- 下載「免費的」[**SQL Server 2016 Developer Edition！**](https://www.microsoft.com/en-us/cloud-platform/sql-server-editions-developers)
- 下載最新版的 [SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md)。 
- 有 Azure 帳戶嗎？ 啟動[已安裝 SQL Server 2016 的虛擬機器](https://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2016sp1standardwindowsserver2016/)。

## <a name="sql-server-2016-database-engine"></a>SQL Server 2016 Database Engine
- 您現在可以在 SQL Server 安裝及設定期間，設定「多個 TempDB」資料庫檔案。
- 新的「查詢存放區」可將查詢文字、執行計畫和效能計量儲存於資料庫內，使您可以輕鬆地監視效能問題並進行疑難排解。 儀表板會顯示哪些查詢使用最多時間、記憶體或 CPU 資源。
- 「時態表」是記錄所有資料變更的記錄資料表，能完整記錄發生資料變更的日期和時間。
- 在 SQL Server 中全新內建的「JSON 支援」可支援 JSON 匯入、匯出、剖析和儲存。
- 新的 **PolyBase** 查詢引擎整合了 SQL Server 與 Hadoop 或 Azure Blob 儲存體中的外部資料。 您可以匯入或匯出資料，也可以執行查詢。
- 新的 **Stretch Database** 功能可讓您動態且安全地將本機 SQL Server 資料庫的資料封存到雲端的 Azure SQL 資料庫。 SQL Server 會自動查詢本機資料，以及位於連結資料庫內的遠端資料。 
- **記憶體內 OLTP：** 
    - 現在支援 FOREIGN KEY、UNIQUE 和 CHECK 限制式，以及原生編譯的預存程序 OR、NOT、SELECT DISTINCT、OUTER JOIN，以及 SELECT 中的子查詢。
    - 支援上至 2TB 的資料表 (原本為 256GB)。 
    - 具備針對排序的資料行存放區索引增強功能，以及 Always On 可用性群組支援。
- 新的安全性功能：
    - **Always Encrypted：**啟用時，只有具備加密金鑰的應用程式才能存取 SQL Server 2016 資料庫中加密的敏感性資料。 金鑰一律不會傳遞至 SQL Server。
    - **動態資料遮罩：**如果有在資料表定義中指定，則受遮罩的資料會對大部分的使用者隱藏，且只有具有 UNMASK 權限的使用者可查看完整資料。
    - **資料列層級安全性：**資料存取可限制於資料庫引擎層級，來讓使用者只能看見與他們相關的項目。 

請參閱[資料庫引擎](../database-engine/configure-windows/what-s-new-in-sql-server-2016-database-engine.md)。
## <a name="sql-server-2016-analysis-services-ssas"></a>SQL Server 2016 Analysis Services (SSAS)
SQL Server 2016 Analysis Services 針對以「1200 (含) 相容性層級」為基礎的表格式模型資料庫，能提供更佳的效能、撰寫功能、資料庫管理、篩選、處理及其他優化。
- **[SQL Server R 服務](../advanced-analytics/r-services/what-s-new-in-sql-server-r-services.md)**能將用於統計分析的 R 程式設計語言整合到 SQL Server 中。 
- 新的「資料庫一致性檢查程式 (DBCC)」會在內部執行，以偵測可能的資料損毀問題。
- 可即時查詢外部資料而不需事先匯入的「直接查詢」功能，現已支援更多資料來源，包括 Azure SQL、Oracle 和 Teradata。 
- 許多新的「DAX (資料存取運算式) 函式」。
- 新的 **[Microsoft.AnalysisServices.Tabular](http://msdn.microsoft.com/library/microsoft.analysisservices.tabular.aspx)** \(機器翻譯\) 命名空間，可管理表格式模式執行個體和模型。 
- [Analysis Services 管理物件 (AMO)](http://msdn.microsoft.com/library/mt436122.aspx) \(機器翻譯\) 已經重構以包含第二個組件 **Microsoft.AnalysisServices.Core.dll**。

請參閱 [Analysis Services 引擎 (SSAS)](../analysis-services/what-s-new-in-analysis-services.md)。 

## <a name="sql-server-2016-integration-services-ssis"></a>SQL Server 2016 Integration Services (SSIS)
- 支援「Always On 可用性群組」
- **累加套件部署**
- 「Always Encrypted」支援
- 新的 **ssis_logreader** 資料庫層級角色
- 新的「自訂記錄層級」
- 資料流程中「適用於錯誤的資料行名稱」 
- 新的「連接器」
- 支援「Hadoop 檔案系統 (HDFS)」

請參閱 [Integration Services (SSIS)](../integration-services/what-s-new-in-integration-services-in-sql-server-2016.md)。

## <a name="sql-server-2016-master-data-services-mds"></a>SQL Server 2016 Master Data Services (MDS)
- 「衍生階層的改進」，包括遞迴和多對多階層的支援
- 「網域屬性」篩選
- 「實體同步」以在模型間共用實體資料
- 透過「變更集」核准工作流程
- 「自訂索引」以改善查詢效能
- 新的「權限層級」以改善安全性
- 重新設計的「商務規則管理」體驗

請參閱 [Master Data Services (MDS)](../master-data-services/what-s-new-in-master-data-services-mds.md)。

## <a name="sql-server-2016-reporting-services-ssrs"></a>SQL Server 2016 Reporting Services (SSRS)
Microsoft 在此版本中徹底翻新了 Reporting Services。 
- 具有 KPI 功能的新「Web 報表入口網站」
- 新的「行動報表發行工具」
- 「重新設計的報表轉譯引擎」，支援 HTML5 
- 新的樹狀圖和放射環狀圖「圖表類型」 

請參閱 [Reporting Services (SSRS)](../reporting-services/what-s-new-in-sql-server-reporting-services-ssrs.md) \(機器翻譯\)。

## <a name="next-steps"></a>後續步驟   
- [SQL Server 安裝程式](../database-engine/install-windows/installation-for-sql-server-2016.md)   
- [SQL Server 2016 版本資訊](../sql-server/sql-server-2016-release-notes.md) 
- [SQL Server 2016 資料工作表](http://download.microsoft.com/download/C/5/3/C53C3AEF-653C-4598-8721-D522E8AC6A3A/SQL_Server_2016_Everything_Built-In_Datasheet_EN_US.pdf)
- [SQL Server 版本支援的功能](https://msdn.microsoft.com/library/cc645993.aspx)
- [安裝 SQL Server 2016 的硬體與軟體需求](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)
- [從安裝精靈安裝 SQL Server 2016](../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)
- [安裝程式和服務安裝](http://msdn.microsoft.com/library/6df72a78-6b36-4bc1-948e-04b4ebe46094)    
- [新的 SQL PowerShell 模組](https://blogs.technet.microsoft.com/dataplatforminsider/2016/06/30/sql-powershell-july-2016-update/)

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
