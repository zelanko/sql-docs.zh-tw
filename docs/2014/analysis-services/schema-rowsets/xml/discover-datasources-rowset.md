---
title: DISCOVER_DATASOURCES 資料列集 |Microsoft 文件
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
api_name:
- DISCOVER_DATASOURCES
topic_type:
- apiref
helpviewer_keywords:
- DISCOVER_DATASOURCES rowset
ms.assetid: f3ff26ab-a447-416b-ba54-1716df2283de
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 32e7aa7327cce301cc8415f45635fda651d861f2
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36023885"
---
# <a name="discoverdatasources-rowset"></a>DISCOVER_DATASOURCES 資料列集
  傳回可用於伺服器或 Web 服務的 XML for Analysis (XMLA) 提供者資料來源清單。 從應用程式 Web 伺服器的 URL 傳回發行的資料來源。 用戶端可以連接至此清單中的其中一個資料來源。  
  
 如果您呼叫[探索](../../xmla/xml-elements-methods-discover.md)方法`DISCOVER_DATASOURCES`中的列舉值[RequestType](../../xmla/xml-elements-properties/type-element-xmla.md)項目，`Discover`方法會傳回`DISCOVER_DATASOURCES`資料列集。  
  
 **適用於：** 表格式模型、 多維度模型  
  
## <a name="rowset-columns"></a>資料列集資料行  
 用戶端會選取資料來源藉由設定`DataSourceInfo`屬性[屬性](../../xmla/xml-elements-properties/properties-element-xmla.md)連同傳送的項目[命令](../../xmla/xml-elements-properties/command-element-xmla.md)元素[Execute](../../xmla/xml-elements-methods-execute.md)方法。 用戶端不應該建構要傳送至伺服器的 `DataSourceInfo` 屬性內容。 用戶端應該改用 `Discover` 方法，來尋找提供者支援的資料來源。 然後，用戶端會針對它從 `DataSourceInfo` 資料列集中擷取的 `DISCOVER_DATASOURCES` 屬性，傳回相同的值。  
  
 `DISCOVER_DATASOURCES`資料列集包含下列資料行。  
  
|資料行名稱|類型指標|限制|描述|  
|-----------------|--------------------|-----------------|-----------------|  
|`DataSourceName`|`DBTYPE_WSTR`|是|資料來源的名稱，例如 `Adventure Works`。|  
|`DataSourceDescription`|`DBTYPE_WSTR`||發行者輸入的資料來源描述。<br /><br /> 可能會傳回 `NULL`。|  
|`URL`|`DBTYPE_WSTR`|是|顯示在哪裡為該資料來源叫用 XML for Analysis (XMLA) 方法的唯一路徑。<br /><br /> 可能會傳回 `NULL`。|  
|`DataSourceInfo`|`DBTYPE_WSTR`||包含連接至資料來源所需的任何其他資訊之字串。<br /><br /> 可能會傳回 `NULL`。|  
|`ProviderName`|`DBTYPE_WSTR`|是|資料來源的提供者名稱。<br /><br /> 範例：`"MSOLAP"`<br /><br /> 可能會傳回 `NULL`。|  
|`ProviderType`|`DBTYPE_WSTR`|是|提供者支援的資料類型。 此陣列可包含下列一個或多個類型：<br /><br /> `MDP`：多維度資料提供者。<br /><br /> `TDP`：表格式資料提供者。<br /><br /> `DMP`：資料採礦提供者 (實作 OLE for DB for Data Mining 規格)。|  
|`AuthenticationMode`|`DBTYPE_WSTR`|是|資料來源使用哪個類型之安全性模式的規格。 它可以是下列其中一個值：<br /><br /> `Unauthenticated`：不必傳送使用者識別碼或是密碼。<br /><br /> `Authenticated`：使用者識別碼與密碼必須包括在連接至資料來源所需的資訊中。<br /><br /> `Integrated`：資料來源會使用基礎安全性來決定授權，例如 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Internet Information Services (IIS) 提供的整合式安全性。|  
  
 這個結構描述資料列集並未排序。  
  
> [!IMPORTANT]  
>  `DISCOVER_DATASOURCES` 資料列集無法使用 DMV 查詢和 SELECT 命令語法來查詢。 不過，`DISCOVER_DATASOURCES` 資料列集可以使用 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.GetSchemaDataSet%2A> 來查詢。  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>使用 ADOMD.NET 傳回資料列集  
 使用 ADOMD.NET 和結構描述資料列集來擷取中繼資料時，您可以使用 GUID 或字串，在 GetSchemaDataSet 方法中參考結構描述資料列集物件。 如需詳細資訊，請參閱 [Working with Schema Rowsets in ADOMD.NET](../../../relational-databases/native-client-ole-db-rowsets/rowsets.md)。  
  
 下表將提供可識別此資料列集的 GUID 和字串值。  
  
|引數|ReplTest1|  
|--------------|-----------|  
|GUID|06c03d41-f66d-49f3-b1b8-987f7af4cf18|  
|ADOMDNAME|DataSources|  
  
## <a name="see-also"></a>另請參閱  
 [XML for Analysis 結構描述資料列集](xml-for-analysis-schema-rowsets.md)  
  
  