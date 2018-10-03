---
title: 支援的資料來源 (SSAS 表格式) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: d6c2b1b3-91fc-4175-af25-509946dc7f24
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 606d597bd539da9e50b1c0452d9126e2f4671731
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48054368"
---
# <a name="data-sources-supported-ssas-tabular"></a>Data Sources Supported (SSAS Tabular)
  此主題描述可以搭配表格式模型使用之資料來源的類型。  
  
 本文包含下列各節：  
  
-   [支援的資料來源](#bkmk_supported_ds)  
  
-   [不支援的來源](#bkmk_unsupported_ds)  
  
-   [選擇資料來源的秘訣](#bkmk_tips)  
  
##  <a name="bkmk_supported_ds"></a> 支援的資料來源  
 您可以從下表的資料來源匯入資料。 當您安裝 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]時，安裝程式不會安裝所列每種資料來源的提供者。 某些提供者可能已經隨著其他應用程式安裝在您的電腦上。在其他情況下，您將需要下載和安裝提供者。  
  
|||||  
|-|-|-|-|  
|來源|版本|檔案類型|提供者<sup>1</sup>|  
|Access 資料庫|Microsoft Access 2003、 2007、 2010 年。|.accdb 或 .mdb|ACE 14 OLE DB 提供者|  
|SQL Server 關聯式資料庫|Microsoft SQL server 2005、 2008、 2008 R2SQL Server 2012，Microsoft SQL Azure 資料庫<sup>2</sup>|(不適用)|OLE DB Provider for SQL Server<br /><br /> SQL Server Native Client OLE DB 提供者<br /><br /> SQL Server Native 10.0 Client OLE DB 提供者<br /><br /> .NET Framework Data Provider for SQL Client|  
|SQL Server Parallel Data Warehouse (PDW) <sup>3</sup>|2008 R2|(不適用)|OLE DB Provider for SQL Server PDW|  
|Oracle 關聯式資料庫|Oracle 9i、10g、11g。|(不適用)|Oracle OLE DB Provider<br /><br /> .NET Framework Data Provider for Oracle Client<br /><br /> .NET Framework Data Provider for SQL Server<br /><br /> OraOLEDB<br /><br /> MSDASQL|  
|Teradata 關聯式資料庫|Teradata V2R6、V12|(不適用)|TDOLEDB OLE DB 提供者<br /><br /> .Net Data Provider for Teradata|  
|Informix 關聯式資料庫||(不適用)|Informix OLE DB 提供者|  
|IBM DB2 關聯式資料庫|8.1|(不適用)|DB2OLEDB|  
|Sybase Adaptive Server Enterprise (ASE) 關聯式資料庫|15.0.2|(不適用)|Sybase OLE DB 提供者|  
|其他關聯式資料庫|(不適用)|(不適用)|OLE DB 提供者或 ODBC 驅動程式|  
|文字檔|(不適用)|.txt、.tab、.csv|Microsoft Access 的 ACE 14 OLE DB 提供者|  
|Microsoft Excel 檔案|Excel 97-2003、2007、2010|.xlsx、xlsm、.xlsb、.xltx、.xltm|ACE 14 OLE DB 提供者|  
|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 活頁簿|Microsoft SQL Server 2008 R2 Analysis Services|.xlsx、xlsm、.xlsb、.xltx、.xltm|ASOLEDB 10.5<br /><br /> (僅搭配發行至已安裝 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 之 SharePoint 伺服陣列的 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 活頁簿使用)|  
|Analysis Services Cube|Microsoft SQL Server 2005、2008、2008 R2 Analysis Services|(不適用)|ASOLEDB 10|  
|資料摘要<br /><br /> (用來匯入 Reporting Services 報表、Atom 服務文件、Microsoft Azure Marketplace DataMarket 和單一資料摘要的資料)|Atom 1.0 格式<br /><br /> 任何公開為 Windows Communication Foundation (WCF) Data Service (先前稱為 ADO.NET Data Services) 的資料庫或文件。|定義一個或多個摘要之服務文件的 .atomsvc<br /><br /> Atom Web 摘要文件的 .atom|Microsoft Data Feed Provider for [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]<br /><br /> 適用於 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]|  
|Office 資料庫連線檔案||.odc||  
  
 <sup>1</sup>您也可以使用 OLE DB Provider for ODBC。  
  
 <sup>2</sup>如需有關 SQL Azure 的詳細資訊，請參閱網站[SQL Azure](http://go.microsoft.com/fwlink/?LinkID=157856)。  
  
 <sup>3</sup>如需有關 SQL Server PDW 的詳細資訊，請參閱網站[SQL Server 2008 R2 Parallel Data Warehouse](http://go.microsoft.com/fwlink/?LinkId=150895)。  
  
 <sup>4</sup>在某些情況下，使用 MSDAORA OLE DB 提供者可能會造成連接錯誤，特別是使用較新版本的 Oracle。 若一旦遭遇任何錯誤，建議您改用列於 Oracle 底下的任一其他提供者。  
  
##  <a name="bkmk_unsupported_ds"></a> 不支援的來源  
 目前不支援下列資料來源：  
  
-   無法匯入伺服器文件，例如，已發行到 SharePoint 的 Access 資料庫。  
  
##  <a name="bkmk_tips"></a> 選擇資料來源的秘訣  
  
1.  從關聯式資料庫匯入資料表可以省去一些步驟，因為在匯入期間，會使用 *外部索引鍵* (Foreign key) 關聯性來建立模型設計師中資料表之間的關聯性。  
  
2.  匯入多個資料表，然後刪除不需要的資料表，也可以省去一些步驟。 如果您一次匯入一個資料表，則可能仍然需要以手動方式建立資料表之間的關聯性。  
  
3.  包含不同資料來源中類似資料的資料行是在模型設計師中建立關聯性的基礎。 使用異質性資料來源時，所選擇之資料表應該具有資料行，可對應至包含相同或相似資料的其他資料來源中資料表。  
  
4.  OLE DB 提供者有時候可能會針對大規模的資料提供更快的效能。 為相同的資料來源在不同的提供者之間選擇時，您應該先嘗試 OLE DB 提供者。  
  
## <a name="see-also"></a>另請參閱  
 [資料來源&#40;SSAS 表格式&#41;](../data-sources-ssas-tabular.md)   
 [匯入資料&#40;SSAS 表格式&#41;](../import-data-ssas-tabular.md)  
  
  
