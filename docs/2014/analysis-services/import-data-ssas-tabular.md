---
title: 匯入資料（SSAS 表格式） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 6617b2a2-9f69-433e-89e0-4c5dc92982cf
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b7eb3fe1157ba40466cc619f504255084aa845fa
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66080620"
---
# <a name="import-data-ssas-tabular"></a>匯入資料 (SSAS 表格式)
  您可以從許多不同的來源，將資料匯入表格式模型中。 本節的主題描述如何使用資料匯入精靈連接至資料，以及選取要匯入模型專案的資料。  
  
> [!IMPORTANT]  
>  如果模型中的任何資料表將包含大量資料列，請考慮只在模型撰寫期間匯入某個資料子集。 您可以藉由匯入資料子集來減少處理時間及工作區資料庫伺服器資源的耗用量。  
  
 您可以使用資料表匯入精靈，從下列資料來源匯入資料：  
  
|**資料來源**|**說明**|  
|---------------------|---------------------|  
|**關聯式資料庫**|關聯式資料來源包括：<br /><br /> Microsoft SQL Server<br /><br /> Microsoft SQL Azure<br /><br /> Microsoft SQL Server Parallel Data Warehouse<br /><br /> Microsoft Access<br /><br /> Oracle<br /><br /> Teradata<br /><br /> Sybase<br /><br /> Informix<br /><br /> IBM DB2<br /><br /> OLEDB/ODBC|  
|**多維度來源**|Microsoft SQL Server Analysis Services Cube|  
|**資料摘要**|資料摘要包括：<br /><br /> Microsoft Reporting Services 報表<br /><br /> Azure DataMarket 資料集<br /><br /> 公用提供者或公司提供者的 ATOM 摘要|  
|**文字檔**|文字檔包括：<br /><br /> Excel 檔案 (.xlsx)<br /><br /> 文字檔 (.txt)|  
  
 除了使用資料表匯入精靈匯入資料之外，您還可以將複製的資料 (從 [剪貼簿]) 貼到資料表中。 貼上的資料在運作上會與從其他資料來源匯入的資料不同。 在資料表中貼上的資料不具備 [連接名稱] 或 [來源資料] 屬性。 貼上的資料保存於 Model.bim 檔中。 儲存專案或 Model.bim 檔時，也會儲存貼上的資料。  
  
## <a name="related-tasks"></a>相關工作  
  
|主題|描述|  
|-----------|-----------------|  
|[從關聯式資料來源匯入 &#40;SSAS 表格式&#41;](import-from-a-relational-data-source-ssas-tabular.md)|描述如何從 Microsoft SQL Server、Oracle 或 Teradata 資料庫等關聯式資料來源匯入資料。|  
|[從多維度資料來源匯入 &#40;SSAS 表格式&#41;](import-from-a-multidimensional-data-source-ssas-tabular.md)|描述如何從多維度 SQL Server Analysis Services Cube 匯入資料。|  
|[從資料摘要匯入 &#40;SSAS 表格式&#41;](import-from-a-data-feed-ssas-tabular.md)|描述如何從 Microsoft Reporting Services 報表或 Azure DataMarket 資料集等資料摘要匯入資料。|  
|[從 &#40;SSAS 表格式&#41;的文字檔匯入](import-from-a-text-file-ssas-tabular.md)|描述如何從 Microsoft Excel 活頁簿或文字檔匯入資料。|  
|[複製並貼上資料 &#40;SSAS 表格式&#41;](copy-and-paste-data-ssas-tabular.md)|描述如何使用 [貼上] 和 [貼上新增]，將資料加入模型設計師中的現有資料表。|  
  
  
