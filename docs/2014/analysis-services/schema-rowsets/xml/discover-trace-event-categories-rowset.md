---
title: DISCOVER_TRACE_EVENT_CATEGORIES 資料列集 |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 1ad74fd2-4740-469d-85b5-abf0171737fd
caps.latest.revision: 6
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: f447e0acbdc2f5e5cbcbf7d3773330cfc9cd39e8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36022494"
---
# <a name="discovertraceeventcategories-rowset"></a>DISCOVER_TRACE_EVENT_CATEGORIES 資料列集
  顯示追蹤提供者所支援之事件類別目錄的清單。  
  
 **適用於：** 表格式模型、 多維度模型  
  
## <a name="rowset-columns"></a>資料列集資料行  
 `DISCOVER_TRACE_EVENT_CATEGORIES`資料列集包含下列資料行。  
  
|資料行名稱|類型指標|長度|描述|  
|-----------------|--------------------|------------|-----------------|  
|`Data`|`DBTYPE_WSTR`||包含編碼的 XML 字串，其中描述追蹤提供者的事件類別目錄相關資訊，包括類別目錄名稱、類型和描述。 類型是表示事件類別目錄類型的字串。 列舉值如下：<br /><br /> -0 = 正常<br />-1 = 有效<br />-2 = 錯誤|  
  
 這個結構描述資料列集並未排序。  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>使用 ADOMD.NET 傳回資料列集  
 使用 ADOMD.NET 和結構描述資料列集來擷取中繼資料時，您可以使用 GUID 或字串，在 GetSchemaDataSet 方法中參考結構描述資料列集物件。 如需詳細資訊，請參閱 [Working with Schema Rowsets in ADOMD.NET](../../../relational-databases/native-client-ole-db-rowsets/rowsets.md)。  
  
 下表將提供可識別此資料列集的 GUID 和字串值。  
  
|引數|ReplTest1|  
|--------------|-----------|  
|GUID|a07ccd19-8148-11d0-87bb-00c04fc33942|  
|String|DISCOVER_TRACE_EVENT_CATEGORIES|  
  
## <a name="see-also"></a>另請參閱  
 [XML for Analysis 結構描述資料列集](xml-for-analysis-schema-rowsets.md)  
  
  