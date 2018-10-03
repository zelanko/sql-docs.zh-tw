---
title: OLE DB for OLAP 結構描述資料列 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- schema rowsets [Analysis Services], OLE DB for OLAP
- OLE DB for OLAP schema rowsets
- schema rowsets [OLE DB for OLAP]
- rowsets [Analysis Services], OLE DB for OLAP
ms.assetid: 5fad3ecc-407c-4148-862e-ea6119cc7480
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bd2e29e03617ccc3929ca0845e2b703e406cbfb2
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48172968"
---
# <a name="ole-db-for-olap-schema-rowsets"></a>OLE DB for OLAP 結構描述資料列集
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] XML for Analysis (XMLA) 提供者支援下列的 OLE DB for OLAP 結構描述資料列集。  
  
> [!NOTE]  
>  若要檢查的特定資料來源提供者是否支援資料列集，請使用`DISCOVER_ENUMERATIONS`資料列集搭配[Discover](../../xmla/xml-elements-methods-discover.md)方法。  
  
 您也可以找到所搜尋主題，也就是 「 OLAP 結構描述資料列 」，這些資料列集的詳細的資訊，位於 MSDN Library，這[Microsoft 寍鯚](http://go.microsoft.com/fwlink/?LinkId=15426)。  
  
## <a name="in-this-section"></a>本節內容  
  
|結構描述資料列集<sup>1</sup>|描述|  
|-------------------------------|-----------------|  
|[DISCOVER_INSTANCES 資料列集](discover-instances-rowset.md)|描述伺服器上的執行個體。|  
|[DISCOVER_KEYWORDS 資料列集&#40;OLE DB for OLAP&#41;](discover-keywords-rowset-ole-db-for-olap.md)|列舉提供者所保留字詞的清單。|  
|[MDSCHEMA_ACTIONS 資料列集](mdschema-actions-rowset.md)|描述可用於用戶端應用程式的動作。|  
|[MDSCHEMA_CUBES 資料列集](mdschema-cubes-rowset.md)|描述資料庫內 Cube 的結構。|  
|[MDSCHEMA_DIMENSIONS 資料列集](mdschema-dimensions-rowset.md)|描述資料庫內的共用和私人維度。|  
|[MDSCHEMA_FUNCTIONS 資料列集](mdschema-functions-rowset.md)|描述可用於與資料庫相連接的用戶端應用程式的函數。|  
|[MDSCHEMA_HIERARCHIES 資料列集](mdschema-hierarchies-rowset.md)|描述包含在特定維度中的每個階層。|  
|[MDSCHEMA_INPUT_DATASOURCES 資料列集](mdschema-input-datasources-rowset.md)|說明在資料庫內定義的資料來源。|  
|[MDSCHEMA_KPIS 資料列集](mdschema-kpis-rowset.md)|描述資料庫內的關鍵效能指標 (KPI)。|  
|[MDSCHEMA_LEVELS 資料列集](mdschema-levels-rowset.md)|描述特定階層內的每個層級。|  
|[MDSCHEMA_MEASUREGROUP_DIMENSIONS 資料列集](mdschema-measuregroup-dimensions-rowset.md)|列舉量值群組的維度。|  
|[MDSCHEMA_MEASUREGROUPS 資料列集](mdschema-measuregroups-rowset.md)|描述資料庫內的量值群組。|  
|[MDSCHEMA_MEASURES 資料列集](mdschema-measures-rowset.md)|描述 Cube 內的每個量值。|  
|[MDSCHEMA_MEMBERS 資料列集](mdschema-members-rowset.md)|描述資料庫內的成員。|  
|[MDSCHEMA_PROPERTIES 資料列集](mdschema-properties-rowset.md)|描述資料庫內的成員屬性。|  
|[MDSCHEMA_SETS 資料列集](mdschema-sets-rowset.md)|描述目前定義於資料庫中的任何集合，包括工作階段範圍集。|  
  
 <sup>1</sup>的 MSOLAP 資料來源提供者支援此處所列的所有結構描述資料列[!INCLUDE[msCoName](../../../includes/msconame-md.md)]XMLA 提供者。  
  
## <a name="see-also"></a>另請參閱  
 [DISCOVER_ENUMERATORS 資料列集](../xml/discover-enumerators-rowset.md)   
 [Analysis Services 結構描述資料列集](../../schema-rowsets/analysis-services-schema-rowsets.md)  
  
  
