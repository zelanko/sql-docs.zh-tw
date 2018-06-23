---
title: OLE DB for OLAP 結構描述資料列 |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- schema rowsets [Analysis Services], OLE DB for OLAP
- OLE DB for OLAP schema rowsets
- schema rowsets [OLE DB for OLAP]
- rowsets [Analysis Services], OLE DB for OLAP
ms.assetid: 5fad3ecc-407c-4148-862e-ea6119cc7480
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 898749e17cb5b85e61a2b2c3a94b7247a7ab219b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36035340"
---
# <a name="ole-db-for-olap-schema-rowsets"></a>OLE DB for OLAP 結構描述資料列集
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] XML for Analysis (XMLA) 提供者支援下列的 OLE DB for OLAP 結構描述資料列集。  
  
> [!NOTE]  
>  若要檢查特定資料來源提供者是否支援資料列集，請使用`DISCOVER_ENUMERATIONS`含有資料列集[探索](../../xmla/xml-elements-methods-discover.md)方法。  
  
 您也可以找到藉由搜尋 「 OLAP 結構描述資料列集，"主題，這些資料列集的詳細的資訊，在此 MSDN Library 中[Microsoft 寍鯚](http://go.microsoft.com/fwlink/?LinkId=15426)。  
  
## <a name="in-this-section"></a>本節內容  
  
|結構描述資料列<sup>1</sup>|描述|  
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
  
 <sup>1</sup>此處所列的所有結構描述資料列的 MSOLAP 資料來源提供者支援[!INCLUDE[msCoName](../../../includes/msconame-md.md)]XMLA 提供者。  
  
## <a name="see-also"></a>另請參閱  
 [DISCOVER_ENUMERATORS 資料列集](../xml/discover-enumerators-rowset.md)   
 [Analysis Services 結構描述資料列集](../../schema-rowsets/analysis-services-schema-rowsets.md)  
  
  