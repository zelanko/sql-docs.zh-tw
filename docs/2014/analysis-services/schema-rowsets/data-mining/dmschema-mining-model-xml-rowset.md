---
title: DMSCHEMA_MINING_MODEL_XML 資料列集 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- DMSCHEMA_MINING_MODEL_XML
topic_type:
- apiref
helpviewer_keywords:
- DMSCHEMA_MINING_MODEL_XML rowset
ms.assetid: f58b00e9-3f72-4cff-b448-21a9fb529772
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3be57336379c66577c245a891e047ec95f763fd9
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48130818"
---
# <a name="dmschemaminingmodelxml-rowset"></a>DMSCHEMA_MINING_MODEL_XML 資料列集
  傳回採礦模型的 XML 結構。 XML 字串的格式是遵循預測模型標記語言 (PMML 2.1) 標準。  
  
## <a name="rowset-columns"></a>資料列集資料行  
 `DMSCHEMA_MINING_MODEL_XML`資料列集包含下列資料行。  
  
|資料行名稱|類型指標|長度|描述|  
|-----------------|--------------------|------------|-----------------|  
|`MODEL_CATALOG`|`DBTYPE_WSTR`||目錄的名稱。 以模型所屬的資料庫名稱來擴展。|  
|`MODEL_SCHEMA`|`DBTYPE_WSTR`||不合格的結構描述名稱。 不支援此資料行[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; 它一律包含`NULL`。|  
|`MODEL_NAME`|`DBTYPE_WSTR`||模型名稱。 這個資料行不能包含 `NULL`。|  
|`MODEL_TYPE`|`DBTYPE_WSTR`||模型類型。 它是一個提供者特定的字串。 它可以是 `NULL`。|  
|`MODEL_GUID`|`DBTYPE_GUID`||識別模型的 GUID。 不使用 GUID 來識別資料表的提供者會傳回 `NULL`。|  
|`MODEL_PMML`|`DBTYPE_WSTR`||PMML 格式之模型內容的 XML 表示。|  
|`SIZE`|`DBTYPE_UI4`||在 XML 字串中的位元組數目。|  
|`LOCATION`|`DBTYPE_WSTR`||XML 檔案的位置。 如果實體檔案不是用於儲存，則為 `NULL`。|  
  
 這個結構描述資料列集並未排序。  
  
## <a name="restriction-columns"></a>限制資料行  
 在下表列出的資料行上可能會限制 DMSCHEMA_MINING_MODEL_XML 資料列集。  
  
|資料行名稱|類型指標|限制狀態|  
|-----------------|--------------------|-----------------------|  
|`MODEL_CATALOG`|`DBTYPE_W`STR|選擇性。|  
|`MODEL_SCHEMA`|`DBTYPE_WSTR`|選擇性。|  
|`MODEL_NAME`|`DBTYPE_WSTR`|選擇性。|  
|`MODEL_TYPE`|`DBTYPE_WSTR`|選擇性。|  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦結構描述資料列集](../../schema-rowsets/data-mining/data-mining-schema-rowsets.md) 
  
  
