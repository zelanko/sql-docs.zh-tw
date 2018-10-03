---
title: DISCOVER_PERFORMANCE_COUNTERS 資料列集 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
ms.assetid: 62b1e967-af67-4915-a305-727bffd61fe4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d3f4f27d074ff01f02cc05c165e8acb1ea109198
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48129238"
---
# <a name="discoverperformancecounters-rowset"></a>DISCOVER_PERFORMANCE_COUNTERS 資料列集
  傳回一個或多個效能計數器的值。 它不支援隨著時間傳回使用量相關資訊的計數器 (例如每秒磁碟讀取次數以及 CPU 使用量的百分比)。  
  
 **適用於：** 表格式模型、 多維度模型  
  
## <a name="rowset-columns"></a>資料列集資料行  
 `DISCOVER_PERFORMANCE_COUNTERS`資料列集包含下列資料行。  
  
|資料行名稱|類型指標|限制|描述|  
|-----------------|--------------------|-----------------|-----------------|  
|`PERF_COUNTER_NAME`|`DBTYPE_WSTR`|必要項|效能計數器的名稱。|  
|`PERF_COUNTER_VALUE`|`DBTYPE_DOUBLE`||效能計數器的值。|  
  
 這個結構描述資料列集並未排序。  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>使用 ADOMD.NET 傳回資料列集  
 使用 ADOMD.NET 和結構描述資料列集來擷取中繼資料時，您可以使用 GUID 或字串，在 GetSchemaDataSet 方法中參考結構描述資料列集物件。 如需詳細資訊，請參閱 [Working with Schema Rowsets in ADOMD.NET](../../../relational-databases/native-client-ole-db-rowsets/rowsets.md)。  
  
 下表將提供可識別此資料列集的 GUID 和字串值。  
  
|引數|值|  
|--------------|-----------|  
|GUID|a07ccd2e-8148-11d0-87bb-00c04fc33942|  
|ADOMDNAME|PerformanceCounters|  
  
## <a name="see-also"></a>另請參閱  
 [XML for Analysis 結構描述資料列集](xml-for-analysis-schema-rowsets.md)  
  
  
