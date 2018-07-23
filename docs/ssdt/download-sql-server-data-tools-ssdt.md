---
title: 下載 SQL Server Data Tools (SSDT) | Microsoft Docs
ms.custom: ''
ms.date: 07/02/2018
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssdt
ms.reviewer: ''
ms.suite: sql
ms.technology: ssdt
ms.tgt_pltfrm: ''
ms.topic: conceptual
keywords:
- 安裝 SSDT, 下載 SSDT, 最新的 SSDT
ms.assetid: b0fc4987-d260-4d0a-9dd1-98099835b361
caps.latest.revision: 113
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 78eb769a8f37ca055628a89aeebe7dd444673434
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "37988220"
---
# <a name="download-and-install-sql-server-data-tools-ssdt-for-visual-studio"></a>下載並安裝 SQL Server Data Tools (SSDT) for Visual Studio
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md.md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
**SQL Server Data Tools** 是一款新式開發工具，可用來建置 SQL Server 關聯式資料庫、Azure SQL 資料庫、Analysis Services (AS) 資料模型、Integration Services (IS) 套件和 Reporting Services (RS) 報表。 有了 SSDT，您便可設計和部署任何 SQL Server 內容類型，就像在 Visual Studio 中開發應用程式一樣容易。

*對於大多數使用者而言，SQL Server Data Tools (SSDT) 會在 Visual Studio 安裝期間安裝。使用 Visual Studio 安裝程式安裝 SSDT 會新增基本 SSDT 功能，因此您仍然需要執行 [SSDT 獨立安裝程式](#ssdt-for-vs-2017-standalone-installer)以取得 AS、IS 和 RS 工具。*

## <a name="install-ssdt-with-visual-studio-2017"></a>使用 Visual Studio 2017 安裝 SSDT

若要在 [Visual Studio 安裝](https://docs.microsoft.com/visualstudio/install/install-visual-studio)期間安裝 SSDT，請選取 [Data storage and processing] \(資料儲存和處理\) 工作負載，然後選取 [SQL Server Data Tools]。 如果已安裝 Visual Studio，您可以[編輯工作負載清單](https://docs.microsoft.com/visualstudio/install/modify-visual-studio)來包含 SSDT：![資料儲存和處理工作負載](../ssdt/media/download-sql-server-data-tools-ssdt/data-workload.png)



## <a name="install-analysis-services-integration-services-and-reporting-services-tools"></a>安裝 Analysis Services、Integration Services 和 Reporting Services 工具
若要安裝 AS、IS 和 RS 專案支援，請執行 [SSDT 獨立安裝程式](#ssdt-for-vs-2017-standalone-installer)。 

此安裝程式會列出可新增 SSDT 工具的 Visual Studio 執行個體。 如果未安裝 Visual Studio，請選取 [Install a new SQL Server Data Tools instance] \(安裝新的 SQL Server Data Tools 執行個體\) 會以 Visual Studio 的最小版本安裝 SSDT，但若要獲得最佳體驗，建議搭配使用 SSDT 與 [Visual Studio 的最新版本](https://www.visualstudio.com/downloads)。 

![選取 AS、IS、RS](../ssdt/media/download-sql-server-data-tools-ssdt/select-services.png)



## <a name="ssdt-for-vs-2017-standalone-installer"></a>SSDT for VS 2017 (獨立安裝程式)

[![下載](../ssdt/media/download.png) 下載 SSDT for Visual Studio 2017 (15.7.1) ](https://go.microsoft.com/fwlink/?linkid=875613) 

> [!IMPORTANT]
> - 請先解除安裝「Analysis Services 專案」和「Reporting Services 專案」延伸模組 (如果已安裝)，並關閉所有 VS 執行個體，再安裝 SSDT for Visual Studio 2017 (15.7.1)。
> - 在 Windows 10 上安裝 SSDT 並選擇 [安裝適用於 Visual Studio 2017 執行個體的新 SQL Server Data Tools] 時，請清除任何核取方塊，然後先安裝新的執行個體。 安裝新的執行個體之後，請重新啟動電腦，並再次開啟 SSDT 安裝程式，以繼續安裝。  



**版本資訊**  
  
版本號碼：15.7.1  
組建編號：14.0.16167.0  
發行日期：2018 年 7 月 2 日  

如需變更的完整清單，請參閱[變更記錄](changelog-for-sql-server-data-tools-ssdt.md)。

SSDT for Visual Studio 2017 與 Visual Studio 具有相同的[系統需求](https://docs.microsoft.com/visualstudio/productinfo/vs2017-system-requirements-vs)。  

### <a name="available-languages---ssdt-for-vs-2017"></a>可用語言 - 適用於 VS 2017 的 SSDT

這版**適用於 VS 2017 的 SSDT** 提供下列語言版本：  

[中文 (中華人民共和國)]( https://go.microsoft.com/fwlink/?linkid=875613&clcid=0x804) | 
[中文 (台灣)]( https://go.microsoft.com/fwlink/?linkid=875613&clcid=0x404) | 
[英文 (美國)]( https://go.microsoft.com/fwlink/?linkid=875613&clcid=0x409) | 
[法文]( https://go.microsoft.com/fwlink/?linkid=875613&clcid=0x40c)  
[德文]( https://go.microsoft.com/fwlink/?linkid=875613&clcid=0x407) | 
[義大利文]( https://go.microsoft.com/fwlink/?linkid=875613&clcid=0x410) | 
[日文]( https://go.microsoft.com/fwlink/?linkid=875613&clcid=0x411) | 
[韓文]( https://go.microsoft.com/fwlink/?linkid=875613&clcid=0x412) | 
[葡萄牙文 (巴西)]( https://go.microsoft.com/fwlink/?linkid=875613&clcid=0x416) | 
[俄文]( https://go.microsoft.com/fwlink/?linkid=875613&clcid=0x419) | 
[西班牙文]( https://go.microsoft.com/fwlink/?linkid=875613&clcid=0x40a)  



## <a name="ssdt-for-vs-2015-standalone-installer"></a>SSDT for VS 2015 (獨立安裝程式)

[![下載](../ssdt/media/download.png) 下載適用於 Visual Studio 2015 (17.4) 的 SSDT](https://go.microsoft.com/fwlink/?linkid=863440)

**版本資訊**  
  
版本號碼：17.4

此版本的組建編號：14.0.61712.050
  
如需變更的完整清單，請參閱[變更記錄](changelog-for-sql-server-data-tools-ssdt.md)。

### <a name="available-languages---ssdt-for-vs-2015"></a>可用語言 - 適用於 VS 2015 的 SSDT
  
這版**適用於 VS 2015 的 SSDT** 提供下列語言版本：  

[中文 (中華人民共和國)]( https://go.microsoft.com/fwlink/?linkid=863440&clcid=0x804) | 
[中文 (台灣)]( https://go.microsoft.com/fwlink/?linkid=863440&clcid=0x404) | 
[英文 (美國)]( https://go.microsoft.com/fwlink/?linkid=863440&clcid=0x409) | 
[法文]( https://go.microsoft.com/fwlink/?linkid=863440&clcid=0x40c)  
[德文]( https://go.microsoft.com/fwlink/?linkid=863440&clcid=0x407) | 
[義大利文]( https://go.microsoft.com/fwlink/?linkid=863440&clcid=0x410) | 
[日文]( https://go.microsoft.com/fwlink/?linkid=863440&clcid=0x411) | 
[韓文]( https://go.microsoft.com/fwlink/?linkid=863440&clcid=0x412) | 
[葡萄牙文 (巴西)]( https://go.microsoft.com/fwlink/?linkid=863440&clcid=0x416) | 
[俄文]( https://go.microsoft.com/fwlink/?linkid=863440&clcid=0x419) | 
[西班牙文]( https://go.microsoft.com/fwlink/?linkid=863440&clcid=0x40a)  

### <a name="iso-images---ssdt-for-vs-2015"></a>ISO 映像 - 適用於 VS 2015 的 SSDT

SSDT 的 ISO 映像提供了另一種方式，可讓您用來安裝 SSDT 或設定系統管理安裝點。 ISO 是一個獨立的檔案，內含 SSDT 需要的所有元件，而且隨時啟動下載管理員皆可下載，非常適合網路頻寬有限或不穩的情況使用。 下載後，ISO 可掛載為磁碟機或燒錄至 DVD。

> [!NOTE]
> 現在可使用 VS 2015 17.4 ISO 映像的 SSDT。

[中文 (中華人民共和國)]( https://go.microsoft.com/fwlink/?linkid=863443&clcid=0x804) |
[中文 (台灣)]( https://go.microsoft.com/fwlink/?linkid=863443&clcid=0x404) |
[英文 (美國)]( https://go.microsoft.com/fwlink/?linkid=863443&clcid=0x409) |
[法文]( https://go.microsoft.com/fwlink/?linkid=863443&clcid=0x40c)  
[德文]( https://go.microsoft.com/fwlink/?linkid=863443&clcid=0x407) |
[義大利文]( https://go.microsoft.com/fwlink/?linkid=863443&clcid=0x410) |
[日文]( https://go.microsoft.com/fwlink/?linkid=863443&clcid=0x411) |
[韓文]( https://go.microsoft.com/fwlink/?linkid=863443&clcid=0x412) |
[葡萄牙文 (巴西)]( https://go.microsoft.com/fwlink/?linkid=863443&clcid=0x416) |
[俄文]( https://go.microsoft.com/fwlink/?linkid=863443&clcid=0x419) |
[西班牙文]( https://go.microsoft.com/fwlink/?linkid=863443&clcid=0x40a)



## <a name="supported-sql-versions"></a>支援的 SQL 版本
  
|專案範本|支援的 SQL 平台|  
|-------------------|--------------------|  
關聯式資料庫|  SQL Server 2005* - SQL Server 2017<br> (使用 SSDT 17.x 或適用於 Visual Studio 2017 的 SSDT 來連線至 [Linux 上的 SQL Server](../linux/sql-server-linux-overview.md))<br /><br />Azure SQL Database<br /><br />Azure SQL 資料倉儲 (僅支援查詢；尚不支援資料庫專案)<br /><br />  * SQL Server 2005 支援已被取代，<br /><br /> 請改為官方支援的 SQL 版本|
  |Analysis Services 模型<br /><br />Reporting Services 報表 | SQL Server 2008 – SQL Server 2017|
  |Integration Services 封裝| SQL Server 2012 – SQL Server 2017    |
  
## <a name="dacfx"></a>DacFx
SSDT for Visual Studio 2015 和 SSDT for Visual Studio 2017 都會使用 DacFx 17.4.1：[下載資料層應用程式架構 (DacFx) 17.4.1](https://www.microsoft.com/download/details.aspx?id=56508)。


## <a name="next-steps"></a>後續步驟  
安裝 SSDT 後，請逐步完成這些教學課程，了解如何使用 SSDT 建立資料庫、封裝、資料模型及報表：  

- [專案導向的離線資料庫開發](project-oriented-offline-database-development.md)  
- [SSIS 教學課程：建立簡易 ETL 封裝](../integration-services/ssis-how-to-create-an-etl-package.md)  
- [Analysis Services 教學課程](../analysis-services/analysis-services-tutorials-ssas.md)  
- [建立基本資料表報表 (SSRS 教學課程)](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md)  

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]


## <a name="see-also"></a>另請參閱  
[SSDT MSDN 論壇](https://social.msdn.microsoft.com/Forums/sqlserver/home?forum=ssdt)  
[SSDT 團隊部落格](http://blogs.msdn.com/b/ssdt/)  
[DACFx API 參考](https://msdn.microsoft.com/library/dn645454.aspx)  
[下載 SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md)  