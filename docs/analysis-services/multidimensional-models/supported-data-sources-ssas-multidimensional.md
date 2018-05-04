---
title: 支援的資料來源 (SSAS-多維度) |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 925cff488a4fdce4ca017ec2e5a0f16fe862bfe5
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="supported-data-sources-ssas---multidimensional"></a>支援的資料來源 (SSAS - 多維度)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  此主題描述可用於多維度模型的資料來源類型。  
  
##  <a name="bkmk_supported_ds"></a> 支援的資料來源  
 您可以從下表的資料來源擷取資料。 當您安裝 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]時，安裝程式不會安裝所列每種資料來源的提供者。 某些提供者可能已經隨著其他應用程式安裝在您的電腦上。在其他情況下，您將需要下載和安裝提供者。  
  
> [!NOTE]  
>  協力廠商提供者 (如 Oracle OLE DB 提供者) 在這些協力廠商提供的支援之下，也可能會用於連接到協力廠商資料庫。  
  
|||||  
|-|-|-|-|  
|Source|版本|檔案類型|提供者*|  
|Access 資料庫|Microsoft Access 2010、2013、2016|.accdb 或 .mdb|Microsoft Jet 4.0 OLE DB 提供者|  
|SQL Server 關聯式資料庫*|Microsoft SQL Server 2008、 2008 R2、 2012年、 2014年、 2016、 [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]，Azure SQL 資料倉儲，Microsoft Analytics Platform System (APS)<br /><br /> <br /><br /> 注意︰如需 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] Azure.com [上](http://go.microsoft.com/fwlink/?LinkID=157856)的詳細資訊。<br /><br /> 注意︰ Analytics Platform System (APS) 被稱為 「 為 SQL Server 平行資料倉儲 (PDW)。 從 Analysis Services 連接至 PDW 原本需要特殊資料提供者。 此提供者在 SQL Server 2012 中被取代。 從 SQL Server 2012 開始，將使用 SQL Server Native Client 連接至 PDW/AP。 如需 APS 的詳細資訊，請參閱 [Microsoft Analytics Platform System](http://www.microsoft.com/en-us/server-cloud/products/analytics-platform-system/resources.aspx)網站。|(不適用)|OLE DB Provider for SQL Server<br /><br /> SQL Server Native Client OLE DB 提供者<br /><br /> SQL Server Native 11.0 Client OLE DB Provider<br /><br /> .NET Framework Data Provider for SQL Client|  
|Oracle 關聯式資料庫|Oracle 9i、10g、11g、12g|(不適用)|Oracle OLE DB Provider<br /><br /> .NET Framework Data Provider for Oracle Client<br /><br /> .NET Framework Data Provider for SQL Server<br /><br /> OraOLEDB<br /><br /> MSDASQL|  
|Teradata 關聯式資料庫|Teradata V2R6、V12|(不適用)|TDOLEDB OLE DB 提供者<br /><br /> .Net Data Provider for Teradata|  
|Informix 關聯式資料庫|V11.10|(不適用)|Informix OLE DB 提供者|  
|IBM DB2 關聯式資料庫|8.1|(不適用)|DB2OLEDB|  
|Sybase Adaptive Server Enterprise (ASE) 關聯式資料庫|15.0.2|(不適用)|Sybase OLE DB 提供者|  
|其他關聯式資料庫|(不適用)|(不適用)|OLE DB 提供者|  
  
 \* 多維度方案不支援 ODBC 資料來源。 雖然 Analysis Services 本身會處理連接，但是 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 中用於建立方案的設計工具無法連接至 ODBC 資料來源，即使使用 MSDASQL 驅動程式亦然。 如果您的業務需求包含 ODBC 資料來源，請考慮改為建立表格式方案。  
  
 \*\* 部分功能需要在內部部署環境執行的 SQL Server 關聯式資料庫。 具體而言，回寫和 ROLAP 儲存會要求基礎資料來源為 SQL Server 關聯式資料庫。  
  
## <a name="see-also"></a>另請參閱  
 [支援的資料來源](../../analysis-services/tabular-models/data-sources-supported-ssas-tabular.md)   
 [多維度模型中的資料來源](../../analysis-services/multidimensional-models/data-sources-in-multidimensional-models.md)   
 [多維度模型中的資料來源檢視](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)  
  
  
