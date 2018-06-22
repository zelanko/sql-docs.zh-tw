---
title: DMSCHEMA_MINING_MODEL_CONTENT_PMML 資料列集 |Microsoft 文件
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
api_name:
- DMSCHEMA_MINING_MODEL_CONTENT_PMML
topic_type:
- apiref
helpviewer_keywords:
- DMSCHEMA_MINING_MODEL_CONTENT_PMML rowset
ms.assetid: fa05bb08-a955-4c8d-b57f-ffcd82470220
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 3c90e4dd752726b59e68ad6fb03c9d29327006e3
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36022716"
---
# <a name="dmschemaminingmodelcontentpmml-rowset"></a>DMSCHEMA_MINING_MODEL_CONTENT_PMML 資料列集
  傳回採礦模型的 XML 結構。 XML 字串的格式是遵循預測模型標記語言 (PMML 2.1) 標準。  
  
## <a name="rowset-columns"></a>資料列集資料行  
 `DMSCHEMA_MINING_MODEL_CONTENT_PMML`資料列集包含下列資料行。  
  
|資料行名稱|類型指標|長度|描述|  
|-----------------|--------------------|------------|-----------------|  
|`MODEL_CATALOG`|`DBTYPE_WSTR`||以模型是成員的資料庫名稱來擴展之目錄名稱。|  
|`MODEL_SCHEMA`|`DBTYPE_WSTR`||不合格的結構描述名稱。 不支援此資料行[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; 它一律包含`NULL`。|  
|`MODEL_NAME`|`DBTYPE_WSTR`||模型名稱。 這個資料行不能包含 `NULL`。|  
|`MODEL_TYPE`|`DBTYPE_WSTR`||模型類型。 它是一個提供者特定的字串。 它可以是 `NULL`。|  
|`MODEL_GUID`|`DBTYPE_GUID`||識別模型的 GUID。 不使用 GUID 來識別資料表的提供者會傳回 `NULL`。|  
|`MODEL_PMML`|`DBTYPE_WSTR`||PMML 格式之模型內容的 XML 表示。|  
|`SIZE`|`DBTYPE_UI4`||在 XML 字串中的位元組數目。|  
|`LOCATION`|`DBTYPE_WSTR`||XML 檔案的位置。 如果沒有可用的位置，則為 `NULL`。|  
  
 這個結構描述資料列集並未排序。  
  
## <a name="restriction-columns"></a>限制資料行  
 在下表列出的資料行上可能會限制 `DMSCHEMA_MINING_MODEL_CONTENT_PMML` 資料列集。  
  
|資料行名稱|類型指標|限制狀態|  
|-----------------|--------------------|-----------------------|  
|`MODEL_CATALOG`|`DBTYPE_WSTR`|選擇性。|  
|`MODEL_SCHEMA`|`DBTYPE_WSTR`|選擇性。|  
|`MODEL_NAME`|`DBTYPE_WSTR`|選擇性。|  
|`MODEL_TYPE`|`DBTYPE_WSTR`|選擇性。|  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦結構描述資料列集](../../schema-rowsets/data-mining/data-mining-schema-rowsets.md) 
  
  