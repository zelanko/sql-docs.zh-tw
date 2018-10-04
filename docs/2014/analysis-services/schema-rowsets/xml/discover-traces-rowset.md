---
title: DISCOVER_TRACES 資料列集 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
ms.assetid: 1be6a035-ffc9-489e-9d4d-7391b3e384e2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 26d40f737db108ea2a9f8a9cee05f3ee9503c73c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48168239"
---
# <a name="discovertraces-rowset"></a>DISCOVER_TRACES 資料列集
  提供有關伺服器上目前使用中追蹤的資訊。  
  
 **適用於：** 表格式模型、 多維度模型  
  
## <a name="rowset-columns"></a>資料列集資料行  
 `DISCOVER_TRACES`資料列集包含下列資料行。  
  
|資料行名稱|類型指標|描述|  
|-----------------|--------------------|-----------------|  
|`TraceID`|`DBTYPE_WSTR`|追蹤識別碼。|  
|`TraceName`|`DBTYPE_WSTR`|追蹤名稱。|  
|`LogFileName`|`DBTYPE_WSTR`|追蹤記錄檔名稱。|  
|`LogFileSize`|`DBTYPE_I4`|追蹤記錄檔大小。|  
|`LogFileRollover`|`DBTYPE_BOOL`|若為 true，就表示應該換用記錄檔，否則為 false。|  
|`AutoRestart`|`DBTYPE_BOOL`|若為 true，就表示自動重新啟動選項已啟用，否則為 false。|  
|`CreationTime`|`DBTYPE_TIME`|建立追蹤的日期和時間。|  
|`StopTime`|`DBTYPE_TIME`|追蹤的停止時間。|  
|`Type`|`PF_DBTYPE_WSTR`|追蹤的類型。|  
  
 這個結構描述資料列集並未排序。  
  
## <a name="restriction-columns"></a>限制資料行  
 在下表列出的資料行上可能會限制 `DISCOVER_TRACES` 資料列集。  
  
|資料行名稱|類型指標|限制狀態|  
|-----------------|--------------------|-----------------------|  
|**TraceId**|`DBTYPE_I4`|選擇性。|  
|`Type`|WSTR|選擇性。|  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>使用 ADOMD.NET 傳回資料列集  
 使用 ADOMD.NET 和結構描述資料列集來擷取中繼資料時，您可以使用 GUID 或字串，在 GetSchemaDataSet 方法中參考結構描述資料列集物件。 如需詳細資訊，請參閱 [Working with Schema Rowsets in ADOMD.NET](../../../relational-databases/native-client-ole-db-rowsets/rowsets.md)。  
  
 下表將提供可識別此資料列集的 GUID 和字串值。  
  
|引數|值|  
|--------------|-----------|  
|GUID|a07ccd1a-8148-11d0-87bb-00c04fc33942|  
|String|DISCOVER_TRACES|  
  
## <a name="see-also"></a>另請參閱  
 [XML for Analysis 結構描述資料列集](xml-for-analysis-schema-rowsets.md)  
  
  
