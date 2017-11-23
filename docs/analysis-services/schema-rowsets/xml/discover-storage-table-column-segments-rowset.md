---
title: "DISCOVER_STORAGE_TABLE_COLUMN_SEGMENTS 資料列集 |Microsoft 文件"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: schema-rowsets
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
ms.assetid: 3e514715-9fe6-4e6a-accb-4149ffd7e0bf
caps.latest.revision: "15"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 21fdb446b1d2c8475969cbc89050260d0e09f6b2
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="discoverstoragetablecolumnsegments-rowset"></a>DISCOVER_STORAGE_TABLE_COLUMN_SEGMENTS 資料列集
  提供有關表格式中執行之 Analysis Services 資料庫所用的儲存體資料表資料行和區段層級的資訊或[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]模式。 此資料列集主要用於疑難排解和分析。  
  
 **適用於：** 表格式模型  
  
## <a name="rowset-columns"></a>資料列集資料行  
 **DISCOVER_STORAGE_TABLE_COLUMN_SEGMENTS**資料列集包含下列資料行。  
  
|**資料行名稱**|**類型指標**|**限制**|**說明**|  
|---------------------|------------------------|---------------------|---------------------|  
|**資料庫名稱**|**DBTYPE_WSTR**|是|指定表格式資料庫。<br /><br /> **DISCOVER_STORAGE_TABLE_COLUMN_SEGMENTS**資料列集可能會限制使用此資料行。 如果省略，就會使用目前的資料庫。|  
|**CUBE_NAME**|**DBTYPE_WSTR**|是|模型的名稱。<br /><br /> **DISCOVER_STORAGE_TABLES**資料列集可能會限制使用此資料行。|  
|**MEASURE_GROUP_NAME**|**DBTYPE_WSTR**|是|量值群組的名稱。|  
|**PARTITION_NAME**|**DBTYPE_WSTR**|是|資料分割的名稱。|  
|**DIMENSION_NAME**|**DBTYPE_WSTR**||維度的名稱。|  
|**TABLE_ID**|**DBTYPE_WSTR**||資料表區段的內部識別碼。|  
|**COLUMN_ID**|**DBTYPE_WSTR**||資料行的內部識別碼。|  
|**區段 （_N)**|**DBTYPE_I8**||資料表區段的序號。|  
|**TABLE_PARTTION_NUMBER**|**DBTYPE_I8**||分割區的序號。|  
|**RECORDS_COUNT**|**DBTYPE_I8**||分割區中的記錄數目。|  
|**ALLOCATED_SIZE**|**DBTYPE_UI8**||配置給資料行區段的位元組大小。|  
|**USED_SIZE**|**DBTYPE_UI8**||資料行區段所使用的位元組大小。|  
|**COMPRESSION_TYPE**|**DBTYPE_WSTR**||套用到資料行區段之壓縮的類型。 此值僅供內部使用與客戶支援用途。 Microsoft 不會針對這個資料行發佈有效的值或描述。|  
|**BITS_COUNT**|**DBTYPE_I8**||位元的計數。|  
|**BOOKMARK_BITS_COUNT**|**DBTYPE_I8**||書籤位元的計數。|  
|**VERTIPAQ_STATE**|**DBTYPE_WSTR**||此資料行區段的 VertiPaq 壓縮狀態。 這是下列值之一：<br /><br /> SKIPPED – 已略過 VertiPaq 壓縮。<br /><br /> COMPLETED – VertiPaq 壓縮已順利完成。<br /><br /> TIMEBOXED – VertiPaq 壓縮已限定時間框。|  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>使用 ADOMD.NET 傳回資料列集  
 使用 ADOMD.NET 和結構描述資料列集來擷取中繼資料時，您可以使用 GUID 或字串，在 GetSchemaDataSet 方法中參考結構描述資料列集物件。 如需詳細資訊，請參閱 [Working with Schema Rowsets in ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets.md)。  
  
 下表將提供可識別此資料列集的 GUID 和字串值。  
  
|引數|值|  
|--------------|-----------|  
|GUID|a07ccd45-8148-11d0-87bb-00c04fc33942|  
|ADOMDNAME|StorageSegments|  
  
## <a name="example"></a>範例  
 下列查詢會在目前的資料庫中，傳回與模型屬性 LastName 相關聯的儲存體資料表區段。  
  
```  
SELECT DISTINCT TABLE_ID, COLUMN_ID   
FROM $system.DISCOVER_STORAGE_TABLE_COLUMN_SEGMENTS  
WHERE COLUMN_ID = 'LastName'  
ORDER BY TABLE_ID  
  
```  
  
## <a name="see-also"></a>請參閱＜  
 [Analysis Services 結構描述資料列集](../../../analysis-services/schema-rowsets/analysis-services-schema-rowsets.md)  
  
  
