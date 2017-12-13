---
title: "DISCOVER_STORAGE_TABLES 資料列集 |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
ms.assetid: 13df6f10-8efe-4fe9-83a6-96d108809ed1
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 42b139004de7a10c073991613abcbafb84a31688
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/08/2017
---
# <a name="discoverstoragetables-rowset"></a>DISCOVER_STORAGE_TABLES 資料列集
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]允許用戶端決定在表格式或 SharePoint 模式下執行 Analysis Services 資料庫中所包含的資料表。  
  
## <a name="rowset-columns"></a>資料列集資料行  
 **DISCOVER_STORAGE_TABLES**資料列集包含下列資料行。  
  
|**資料行名稱**|**類型指標**|**長度**|**說明**|  
|---------------------|------------------------|----------------|---------------------|  
|**資料庫名稱**|**DBTYPE_WSTR**||指定包含資料表的資料庫名稱。<br /><br /> **DISCOVER_STORAGE_TABLES**資料列集可能會限制使用此資料行。 如果未使用此資料行來限制資料列集，則會使用目前的資料庫。|  
|**CUBE_NAME**|**DBTYPE_WSTR**||指定包含資料表的 Cube 或模型。<br /><br /> **DISCOVER_STORAGE_TABLES**資料列集可能會限制使用此資料行。|  
|**MEASURE_GROUP_NAME**|**DBTYPE_WSTR**||量值群組的名稱。|  
|**PARTITION_NAME**|**DBTYPE_WSTR**||資料分割的名稱。|  
|**DIMENSION_NAME**|**DBTYPE_WSTR**||維度的名稱。|  
|**TABLE_ID**|**DBTYPE_WSTR**||用來存放資料表屬性之資料表的識別碼。|  
|**TABLE_PARTITIONS_COUNT**|**DBTYPE_ WSTR**||資料表分割區計數。|  
|**HINT_TABLE_TYPE**|**DBTYPE_ WSTR**||資料表類型的提示。|  
|**ROWS_COUNT**|**DBTYPE_UI4**||分割區中的資料列數。|  
|**RIVIOLATION_COUNT**|**DBTYPE_UI4**||具有參考完整性違規的資料列數。|  
  
## <a name="restriction-columns"></a>限制資料行  
 **DISCOVER_STORAGE_TABLES**上表中列出的資料行可能會限制資料列集。  
  
|**資料行名稱**|**類型指標**|**限制狀態**|  
|---------------------|------------------------|---------------------------|  
|**資料庫名稱**|**DBTYPE_WSTR**|選擇性。|  
|**CUBE_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**MEASURE_GROUP_NAME**|**DBTYPE_WSTR**|選擇性|  
|**PARTITION_NAME**|**DBTYPE_WSTR**|選擇性|  
  
## <a name="example"></a>範例  
 下列程式碼範例會從目前連接的預設資料庫中，傳回儲存體資料表的清單，以及每個資料表中的資料列數。  
  
```  
SELECT TABLE_ID, ROWS_COUNT  
FROM $system.DISCOVER_STORAGE_TABLES  
ORDER BY TABLE_ID DESC  
  
```  
  
## <a name="see-also"></a>請參閱  
 [Analysis Services 結構描述資料列集](../../../analysis-services/schema-rowsets/analysis-services-schema-rowsets.md)  
  
  
