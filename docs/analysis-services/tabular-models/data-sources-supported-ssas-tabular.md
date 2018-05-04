---
title: 支援 SQL Server Analysis Services 表格式 1200年模型中的資料來源 |Microsoft 文件
ms.custom: ''
ms.date: 03/28/2018
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: d6c2b1b3-91fc-4175-af25-509946dc7f24
caps.latest.revision: 28
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 1afd2be21af505d0d027567abe1c7d46c956525d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="data-sources-supported-in-sql-server-analysis-services-tabular-1200-models"></a>支援 SQL Server Analysis Services 中表格式 1200年模型的資料來源
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  
本文說明適用於 SQL Server Analysis Services 在 1200年的表格式模型和較低的相容性層級的資料來源的類型。 

若是 1400年相容性層級模型，請參閱[支援 SQL Server Analysis Services 表格式 1400年模型中的資料來源](data-sources-supported-ssas-tabular-1400.md)。

Azure Analysis Services，請參閱[支援 Azure Analysis Services 中的資料來源](https://docs.microsoft.com/azure/analysis-services/analysis-services-datasource)。
  
##  <a name="bkmk_supported_ds"></a> 記憶體中的表格式模型支援的資料來源  
當您安裝 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]時，安裝程式不會安裝所列每種資料來源的提供者。 某些提供者可能會與您的電腦上的其他應用程式安裝。 在其他情況下，您可能需要下載並安裝提供者。  
  
|||||  
|-|-|-|-|  
|Source|版本|檔案類型|提供者|  
|Access 資料庫|Microsoft Access 2010 及更新版本。|.accdb 或 .mdb|ACE 14 OLE DB 提供者|  
|SQL Server 關聯式資料庫|SQL Server 2008 及更新版本、 SQL Server 資料倉儲 2008年和更新版本，Azure SQL Database、 Azure SQL 資料倉儲，Analytics Platform System (APS)<br /><br /> <br /><br /> Analytics Platform System (APS) 被稱為 「 為 SQL Server 平行資料倉儲 (PDW)。 從 Analysis Services 連接至 PDW 原本需要特殊資料提供者。 此提供者在 SQL Server 2012 中被取代。 從 SQL Server 2012 開始，將使用 SQL Server Native Client 連接至 PDW/AP。 |(不適用)|OLE DB Provider for SQL Server<br /><br /> SQL Server Native Client OLE DB 提供者<br /><br /> SQL Server Native 10.0 Client OLE DB 提供者<br /><br /> .NET Framework Data Provider for SQL Client|  
|Oracle 關聯式資料庫|Oracle 9i 和更新版本。|(不適用)|Oracle OLE DB Provider<br /><br /> .NET Framework Data Provider for Oracle Client<br /><br /> .NET Framework Data Provider for SQL Server<br /><br /> OraOLEDB<br /><br /> MSDASQL|  
|Teradata 關聯式資料庫|Teradata V2R6 和更新版本|(不適用)|TDOLEDB OLE DB 提供者<br /><br /> .Net Data Provider for Teradata|  
|Informix 關聯式資料庫||(不適用)|Informix OLE DB 提供者|  
|IBM DB2 關聯式資料庫|8.1|(不適用)|DB2OLEDB|  
|Sybase Adaptive Server Enterprise (ASE) 關聯式資料庫|15.0.2|(不適用)|Sybase OLE DB 提供者|  
|其他關聯式資料庫|(不適用)|(不適用)|OLE DB 提供者或 ODBC 驅動程式|  
|文字檔|(不適用)|.txt、.tab、.csv|Microsoft Access 的 ACE 14 OLE DB 提供者|  
|Microsoft Excel 檔案|Excel 2010 及更新版本|.xlsx、xlsm、.xlsb、.xltx、.xltm|ACE 14 OLE DB 提供者|  
|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 活頁簿|Microsoft SQL Server 2008 和更新版本的 Analysis Services|.xlsx、xlsm、.xlsb、.xltx、.xltm|ASOLEDB 10.5<br /><br /> (僅搭配發行至已安裝 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 之 SharePoint 伺服陣列的 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 活頁簿使用)|  
|Analysis Services Cube|Microsoft SQL Server 2008 和更新版本的 Analysis Services|(不適用)|ASOLEDB 10|  
|資料摘要<br /><br /> (用來匯入 Reporting Services 報表、Atom 服務文件、Microsoft Azure Marketplace DataMarket 和單一資料摘要的資料)|Atom 1.0 格式<br /><br /> 任何公開為 Windows Communication Foundation (WCF) Data Service (先前稱為 ADO.NET Data Services) 的資料庫或文件。|`.atomsvc` 定義一個或多個摘要之服務文件<br /><br /> Atom Web 摘要文件的 .atom|Microsoft Data Feed Provider for [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]<br /><br /> 適用於 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]|  
|Office 資料庫連線檔案||.odc||  
  
  
##  <a name="bkmk_supported_ds_dq"></a> DirectQuery 模型的支援的資料來源  
 DirectQuery 是記憶體內部儲存模式的替代方式，直接從後端資料系統路由傳送查詢和傳回結果，而非在模型內 (和 RAM 中，一旦載入模型) 儲存所有資料。 因為 Analysis Services 來編寫以原生資料庫查詢語法的查詢，此模式支援較小的資料來源子集。  
  
資料來源   |版本  |提供者
---------|---------|---------
Microsoft SQL Server    |  2008 及更新版本      |       OLE DB Provider for SQL Server、SQL Server Native Client OLE DB 提供者、.NET Framework Data Provider for SQL Client  
Microsoft Azure SQL Database    |   全部      |  OLE DB Provider for SQL Server、SQL Server Native Client OLE DB 提供者、.NET Framework Data Provider for SQL Client            
Microsoft Azure SQL 資料倉儲     |   全部     |  SQL Server Native Client OLE DB 提供者、.NET Framework Data Provider for SQL Client       
Microsoft SQL Analytics Platform System (APS)     |   全部      |  OLE DB Provider for SQL Server、SQL Server Native Client OLE DB 提供者、.NET Framework Data Provider for SQL Client       
Oracle 關聯式資料庫     |  Oracle 9i 和更新版本       |  Oracle OLE DB Provider       
Teradata 關聯式資料庫    |  Teradata V2R6 和更新版本     | .Net Data Provider for Teradata    

  
##  <a name="bkmk_tips"></a> 選擇資料來源的秘訣  
  
從關聯式資料庫匯入資料表可以省去一些步驟，因為在匯入期間，會使用 *外部索引鍵* (Foreign key) 關聯性來建立模型設計師中資料表之間的關聯性。  
  
匯入多個資料表，然後刪除不需要的資料表，也可以省去一些步驟。 如果您一次匯入一個資料表，則可能仍然需要以手動方式建立資料表之間的關聯性。  
  
包含不同資料來源中類似資料的資料行是在模型設計師中建立關聯性的基礎。 使用異質性資料來源時，所選擇之資料表應該具有資料行，可對應至包含相同或相似資料的其他資料來源中資料表。  
  
OLE DB 提供者有時候可能提供大規模資料的效能更佳。 為相同的資料來源在不同的提供者之間選擇時，您應該先嘗試 OLE DB 提供者。  

## <a name="see-also"></a>另請參閱

[支援 SQL Server Analysis Services 中表格式 1400年模型的資料來源](data-sources-supported-ssas-tabular-1400.md)

[Azure Analysis Services 中支援的資料來源](https://docs.microsoft.com/azure/analysis-services/analysis-services-datasource)   