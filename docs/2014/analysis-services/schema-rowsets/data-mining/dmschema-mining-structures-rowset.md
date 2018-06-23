---
title: DMSCHEMA_MINING_STRUCTURES 資料列集 |Microsoft 文件
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
- DMSCHEMA_MINING_STRUCTURES
topic_type:
- apiref
helpviewer_keywords:
- DMSCHEMA_MINING_STRUCTURES rowset
ms.assetid: 6224556b-08a0-496e-bd7c-632c3e833e26
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: b61df846e3b9da7301650a8029d12eb72a218049
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36146830"
---
# <a name="dmschemaminingstructures-rowset"></a>DMSCHEMA_MINING_STRUCTURES 資料列集
  列舉在目前目錄中之採礦結構的有關資訊。  
  
## <a name="rowset-columns"></a>資料列集資料行  
 `DMSCHEMA_MINING_STRUCTURES`資料列集包含下列資料行。  
  
|資料行名稱|類型指標|長度|描述|  
|-----------------|--------------------|------------|-----------------|  
|`STRUCTURE_CATALOG`|`DBTYPE_WSTR`||目錄的名稱。|  
|`STRUCTURE_SCHEMA`|`DBTYPE_WSTR`||不合格的結構描述名稱。 如果提供者不支援結構描述，則為 `NULL`。|  
|`STRUCTURE_NAME`|`DBTYPE_WSTR`||結構名稱。 這個資料行不能包含 `NULL`。|  
|`STRUCTURE_GUID`|`DBTYPE_GUID`||唯一識別結構的 GUID。 如果提供者不支援，則為 `NULL`。|  
|`DESCRIPTION`|`DBTYPE_WSTR`||結構的精簡描述。 如果沒有描述與結構關聯，則為 `NULL`。|  
|`STRUCTURE_PROPID`|`DBTYPE_UI4`||結構的屬性識別碼。 如果提供者不支援，則為 `NULL`。|  
|`DATE_CREATED`|`DBTYPE_DBTIMESTAMP`||建立結構時的日期。 如果提供者沒有提供，則為 `NULL`。|  
|`DATE_MODIFIED`|`DBTYPE_DBTIMESTAMP`||最後修改結構時的日期。 如果提供者沒有提供，則為 `NULL`。|  
|`CREATION_STATEMENT`|`DBTYPE_WSTR`||(選擇性) 用以建立原始資料採礦模型的陳述式。|  
|`IS_POPULATED`|`DBTYPE_BOOL`||布林值，指出結構是否已擴展。<br /><br /> 如果結構已擴展，則為 `VARIANT_TRUE`，否則為 `VARIANT_FALSE`。|  
|`LAST_PROCESSED`|`DBTYPE_DBTIMESTAMP`||最後處理結構時的日期。 如果提供者沒有提供，則為 `NULL`。|  
|`HOLDOUT_MAXPERCENT`|`DBTYPE_ UI1`||使用者指定的值，指出當做測試集的輸入案例之最大百分比。<br /><br /> 0 或是 `NULL` 表示沒有限制。|  
|`HOLDOUT_MAXCASES`|`DBTYPE_UI8`||使用者指定的值，指出當做測試集的輸入案例之最大數目。<br /><br /> 0 或是 `NULL` 表示沒有限制。|  
|`HOLDOUT_SEED`|`DBTYPE_UI8`||使用者指定的值，做為可重複資料分割之種子使用。<br /><br /> 0 表示使用採礦結構識別碼的雜湊做為種子。|  
|`HOLDOUT_ACTUAL_SIZE`|`DBTYPE_UI8`||如果採礦結構已處理過，這裡指出的是以案例數目表示的測試資料集實際大小。<br /><br /> `NULL` 表示採礦結構未處理過。|  
  
 資料列集會在 `STRUCTURE_CATALOG`、`STRUCTURE_SCHEMA` 和 `STRUCTURE_NAME` 排序。  
  
## <a name="restriction-columns"></a>限制資料行  
 在下表列出的資料行上可能會限制 `DMSCHEMA_MINING_STRUCTURES` 資料列集。  
  
|資料行名稱|類型指標|限制狀態|  
|-----------------|--------------------|-----------------------|  
|`STRUCTURE_CATALOG`|`DBTYPE_WSTR`|選擇性。|  
|`STRUCTURE_SCHEMA`|`DBTYPE_WSTR`|選擇性。|  
|`STRUCTURE_NAME`|`DBTYPE_WSTR`|選擇性。|  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦結構描述資料列集](../../schema-rowsets/data-mining/data-mining-schema-rowsets.md) 
  
  