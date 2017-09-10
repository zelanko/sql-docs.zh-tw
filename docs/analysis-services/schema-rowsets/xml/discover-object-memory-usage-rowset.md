---
title: "DISCOVER_OBJECT_MEMORY_USAGE 資料列集 |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DISCOVER_OBJECT_MEMORY_USAGE rowset
ms.assetid: 211cfa04-7bd6-43fe-8bd5-bfbff78bdafb
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6bfd0d6517f974b60b3d35f25e5836bcd6a7c8e2
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="discoverobjectmemoryusage-rowset"></a>DISCOVER_OBJECT_MEMORY_USAGE 資料列集
  提供物件使用之記憶體資源的有關資訊。  
  
## <a name="rowset-columns"></a>資料列集資料行  
 **DISCOVER_OBJECT_MEMORY_USAGE**資料列集包含下列資料行。  
  
|資料行名稱|類型指標|長度|Description|  
|-----------------|--------------------|------------|-----------------|  
|**OBJECT_PARENT_PATH**|**DBTYPE_WSTR**||目前物件父系的路徑。|  
|**OBJECT_ID**|**DBTYPE_WSTR**||在建立時定義的物件識別碼。|  
|**OBJECT_MEMORY_SHRINKABLE**|**DBTYPE_I8**||目前物件直接擁有之全部可壓縮物件所使用的記憶體總量 (位元組)。 目前的值並不包括來自目前物件所擁有之具名物件所擁有的物件之記憶體。|  
|**OBJECT_MEMORY_NONSHRINKABLE**|**DBTYPE_I8**||目前物件直接擁有之全部非可壓縮物件的記憶體數量 (位元組)。 目前的值並不包括來自目前物件所擁有之具名物件所擁有的物件之記憶體。|  
|**OBJECT_VERSION**|**DBTYPE_I4**||物件的中繼資料版本號碼。 每次改變物件時，這個號碼就會變更。|  
|**OBJECT_DATA_VERSION**|**DBTYPE_I4**||物件之資料的歷程記錄號碼。 每次處理物件時，這個號碼就會增加。|  
|**OBJECT_TYPE_ID**|**DBTYPE_I4**||保留供內部使用。|  
|**OBJECT_TIME_CREATED**|**DBTYPE_DBTIMESTAMP**||建立物件時的 UTC 伺服器時間。|  
  
 這個結構描述資料列集並未排序。  
  
## <a name="restriction-columns"></a>限制資料行  
 **DISCOVER_OBJECT_MEMORY_USAGE**上表中列出的資料行可能會限制資料列集。  
  
|資料行名稱|類型指標|限制狀態|  
|-----------------|--------------------|-----------------------|  
|**OBJECT_PARENT_PATH**|**DBTYPE_WSTR**|選擇性。|  
|**OBJECT_ID**|**DBTYPE_WSTR**|選擇性|  
  
## <a name="see-also"></a>另請參閱  
 [XML for Analysis 結構描述資料列集](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
