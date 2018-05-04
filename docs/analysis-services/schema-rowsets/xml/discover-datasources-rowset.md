---
title: DISCOVER_DATASOURCES 資料列集 |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- DISCOVER_DATASOURCES
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DISCOVER_DATASOURCES rowset
ms.assetid: f3ff26ab-a447-416b-ba54-1716df2283de
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 79b6cd2e494f35ac87c3483cb0929721eee13e82
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="discoverdatasources-rowset"></a>DISCOVER_DATASOURCES 資料列集
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  傳回可用於伺服器或 Web 服務的 XML for Analysis (XMLA) 提供者資料來源清單。 從應用程式 Web 伺服器的 URL 傳回發行的資料來源。 用戶端可以連接至此清單中的其中一個資料來源。  
  
 如果您呼叫[探索](../../../analysis-services/xmla/xml-elements-methods-discover.md)方法**DISCOVER_DATASOURCES**中的列舉值[RequestType](../../../analysis-services/xmla/xml-elements-properties/requesttype-element-xmla.md)項目，**探索**方法會傳回**DISCOVER_DATASOURCES**資料列集。  
  
 **適用於：**表格式模型、 多維度模型  
  
## <a name="rowset-columns"></a>資料列集資料行  
 用戶端會選取資料來源藉由設定**DataSourceInfo**屬性[屬性](../../../analysis-services/xmla/xml-elements-properties/properties-element-xmla.md)連同傳送的項目[命令](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)元素[Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md)方法。 用戶端不應該建構的內容**DataSourceInfo**屬性傳送到伺服器。 用戶端應該改用**探索**方法來尋找提供者支援的資料來源。 用戶端再傳送回相同的值**DataSourceInfo**屬性，它會從取得**DISCOVER_DATASOURCES**資料列集。  
  
 **DISCOVER_DATASOURCES**資料列集包含下列資料行。  
  
|資料行名稱|類型指標|限制|Description|  
|-----------------|--------------------|-----------------|-----------------|  
|**DataSourceName**|**DBTYPE_WSTR**|是|資料的來源名稱，例如**Adventure Works**。|  
|**DataSourceDescription**|**DBTYPE_WSTR**||發行者輸入的資料來源描述。<br /><br /> 可能會傳回**NULL**。|  
|**URL**|**DBTYPE_WSTR**|是|顯示在哪裡為該資料來源叫用 XML for Analysis (XMLA) 方法的唯一路徑。<br /><br /> 可能會傳回**NULL**。|  
|**DataSourceInfo**|**DBTYPE_WSTR**||包含連接至資料來源所需的任何其他資訊之字串。<br /><br /> 可能會傳回**NULL**。|  
|**ProviderName**|**DBTYPE_WSTR**|是|資料來源的提供者名稱。<br /><br /> 範例：`"MSOLAP"`<br /><br /> 可能會傳回**NULL**。|  
|**提供者類型**|**DBTYPE_WSTR**|是|提供者支援的資料類型。 此陣列可包含下列一個或多個類型：<br /><br /> **MDP**： 多維度資料提供者。<br /><br /> **Tdp，才能在**： 表格式資料提供者。<br /><br /> **DMP**： 資料採礦提供者 （實作 OLE for DB for Data Mining 規格）。|  
|**AuthenticationMode**|**DBTYPE_WSTR**|是|資料來源使用哪個類型之安全性模式的規格。 它可以是下列其中一個值：<br /><br /> **未驗證**： 沒有使用者識別碼或密碼已傳送。<br /><br /> **驗證**： 使用者 ID 和密碼必須包含在連接到資料來源所需的資訊。<br /><br /> **整合式**： 資料來源使用的基礎安全性來決定授權，例如所提供的整合式安全性[!INCLUDE[msCoName](../../../includes/msconame-md.md)]網際網路資訊服務 (IIS)。|  
  
 這個結構描述資料列集並未排序。  
  
> [!IMPORTANT]  
>  **DISCOVER_DATASOURCES**無法使用 DMV 查詢和 SELECT 命令語法來查詢資料列集。 不過， **DISCOVER_DATASOURCES**資料列集可以使用查詢<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.GetSchemaDataSet%2A>。  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>使用 ADOMD.NET 傳回資料列集  
 使用 ADOMD.NET 和結構描述資料列集來擷取中繼資料時，您可以使用 GUID 或字串，在 GetSchemaDataSet 方法中參考結構描述資料列集物件。 如需詳細資訊，請參閱 [Working with Schema Rowsets in ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets.md)。  
  
 下表將提供可識別此資料列集的 GUID 和字串值。  
  
|引數|值|  
|--------------|-----------|  
|GUID|06c03d41-f66d-49f3-b1b8-987f7af4cf18|  
|ADOMDNAME|DataSources|  
  
## <a name="see-also"></a>另請參閱  
 [XML for Analysis 結構描述資料列集](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
