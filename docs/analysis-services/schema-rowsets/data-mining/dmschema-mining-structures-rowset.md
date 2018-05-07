---
title: DMSCHEMA_MINING_STRUCTURES 資料列集 |Microsoft 文件
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5a40c44722108d8377eb98d050f3af528c23c0e5
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="dmschemaminingstructures-rowset"></a>DMSCHEMA_MINING_STRUCTURES 資料列集
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  列舉在目前目錄中之採礦結構的有關資訊。  
  
## <a name="rowset-columns"></a>資料列集資料行  
 **DMSCHEMA_MINING_STRUCTURES**資料列集包含下列資料行。  
  
|資料行名稱|類型指標|長度|Description|  
|-----------------|--------------------|------------|-----------------|  
|**STRUCTURE_CATALOG**|**DBTYPE_WSTR**||目錄的名稱。|  
|**STRUCTURE_SCHEMA**|**DBTYPE_WSTR**||不合格的結構描述名稱。 **NULL**如果提供者不支援結構描述。|  
|**STRUCTURE_NAME**|**DBTYPE_WSTR**||結構名稱。 此資料行不能包含**NULL**。|  
|**STRUCTURE_GUID**|**DBTYPE_GUID**||唯一識別結構的 GUID。 **NULL**如果提供者不支援。|  
|**DESCRIPTION**|**DBTYPE_WSTR**||結構的精簡描述。 **NULL**如果沒有描述與結構相關聯。|  
|**STRUCTURE_PROPID**|**DBTYPE_UI4**||結構的屬性識別碼。 **NULL**如果提供者不支援。|  
|**DATE_CREATED**|**DBTYPE_DBTIMESTAMP**||建立結構時的日期。 **NULL**如果未提供的提供者。|  
|**DATE_MODIFIED**|**DBTYPE_DBTIMESTAMP**||最後修改結構時的日期。 **NULL**如果未提供的提供者。|  
|**CREATION_STATEMENT**|**DBTYPE_WSTR**||(選擇性) 用以建立原始資料採礦模型的陳述式。|  
|**IS_POPULATED**|**DBTYPE_BOOL**||布林值，指出結構是否已擴展。<br /><br /> **VARIANT_TRUE**如果結構已擴展。**VARIANT_FALSE**否則。|  
|**LAST_PROCESSED**|**DBTYPE_DBTIMESTAMP**||最後處理結構時的日期。 **NULL**如果未提供的提供者。|  
|**HOLDOUT_MAXPERCENT**|**DBTYPE_ UI1**||使用者指定的值，指出當做測試集的輸入案例之最大百分比。<br /><br /> 0 或**NULL**表示沒有限制。|  
|**HOLDOUT_MAXCASES**|**DBTYPE_UI8**||使用者指定的值，指出當做測試集的輸入案例之最大數目。<br /><br /> 0 或**NULL**表示沒有限制。|  
|**HOLDOUT_SEED**|**DBTYPE_UI8**||使用者指定的值，做為可重複資料分割之種子使用。<br /><br /> 0 表示使用採礦結構識別碼的雜湊做為種子。|  
|**HOLDOUT_ACTUAL_SIZE**|**DBTYPE_UI8**||如果採礦結構已處理過，這裡指出的是以案例數目表示的測試資料集實際大小。<br /><br /> **NULL**指出不處理採礦結構。|  
  
 排序資料列集**STRUCTURE_CATALOG**， **STRUCTURE_SCHEMA**， **STRUCTURE_NAME**。  
  
## <a name="restriction-columns"></a>限制資料行  
 **DMSCHEMA_MINING_STRUCTURES**上表中列出的資料行可能會限制資料列集。  
  
|資料行名稱|類型指標|限制狀態|  
|-----------------|--------------------|-----------------------|  
|**STRUCTURE_CATALOG**|**DBTYPE_WSTR**|選擇性。|  
|**STRUCTURE_SCHEMA**|**DBTYPE_WSTR**|選擇性。|  
|**STRUCTURE_NAME**|**DBTYPE_WSTR**|選擇性。|  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦結構描述資料列集](../../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)  
  
  
