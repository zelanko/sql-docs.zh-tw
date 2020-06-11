---
title: DISCOVER_XEVENT_TRACE_DEFINITION 資料列集 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
ms.assetid: e1ce2d2d-f994-4318-801a-ee0385aecd84
author: minewiskan
ms.author: owend
ms.openlocfilehash: bedd6ec66a188738ac9a522b4802b3b431e82f36
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84528624"
---
# <a name="discover_xevent_trace_definition-rowset"></a>DISCOVER_XEVENT_TRACE_DEFINITION 資料列集
  提供有關伺服器上目前使用中 XEvent 追蹤的資訊。  
  
 **適用于：** 表格式模型、多維度模型  
  
## <a name="rowset-columns"></a>資料列集資料行  
 `DISCOVER_XEVENT_TRACE_DEFINITION` 資料列集包含下列資料行。  
  
|資料行名稱|類型指標|長度|Description|  
|-----------------|--------------------|------------|-----------------|  
|`Data`|`DBTYPE_WSTR`||XEvent 追蹤的 XML 定義。|  
  
 這個結構描述資料列集並未排序。  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>使用 ADOMD.NET 傳回資料列集  
 使用 ADOMD.NET 和結構描述資料列集來擷取中繼資料時，您可以使用 GUID 或字串，在 GetSchemaDataSet 方法中參考結構描述資料列集物件。 如需詳細資訊，請參閱 [Working with Schema Rowsets in ADOMD.NET](https://docs.microsoft.com/bi-reference/adomd/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets)。  
  
 下表將提供可識別此資料列集的 GUID 和字串值。  
  
|引數|值|  
|--------------|-----------|  
|GUID|a07ccd1c-8148-11d0-87bb-00c04fc33942|  
|String|DISCOVER_XEVENT_TRACE_DEFINITION|  
  
## <a name="see-also"></a>另請參閱  
 [XML for Analysis 架構資料列集](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/xml-for-analysis-schema-rowsets)   
 [使用 SQL Server 擴充事件 &#40;XEvents&#41; 監視 Analysis Services](../instances/monitor-analysis-services-with-sql-server-extended-events.md)   
 [使用動態管理檢視 &#40;DMV&#41; 監視 Analysis Services](../instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services.md)  
  
  
