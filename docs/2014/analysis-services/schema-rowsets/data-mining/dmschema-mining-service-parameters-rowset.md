---
title: DMSCHEMA_MINING_SERVICE_PARAMETERS 資料列集 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- DMSCHEMA_MINING_SERVICE_PARAMETERS
topic_type:
- apiref
helpviewer_keywords:
- DMSCHEMA_MINING_SERVICE_PARAMETERS rowset
ms.assetid: 5994e66b-84d0-4279-9f50-d92fd829dd83
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 85ee3a7833a0c2bffc95ae21b44295d234ee8d5e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48047951"
---
# <a name="dmschemaminingserviceparameters-rowset"></a>DMSCHEMA_MINING_SERVICE_PARAMETERS 資料列集
  描述伺服器上演算法的參數。  
  
## <a name="rowset-columns"></a>資料列集資料行  
 `DMSCHEMA_MINING_SERVICE_PARAMETERS`資料列集包含下列資料行。  
  
|資料行名稱|類型指標|長度|描述|  
|-----------------|--------------------|------------|-----------------|  
|`SERVICE_NAME`|`DBTYPE_WSTR`||演算法的名稱。|  
|`PARAMETER_NAME`|`DBTYPE_WSTR`||參數的名稱。|  
|`PARAMETER_TYPE`|`DBTYPE_WSTR`||參數的類型。|  
|`IS_REQUIRED`|`DBTYPE_BOOL`||如果參數為必要，則為傳回 `TRUE` 的布林值。|  
|`PARAMETER_FLAGS`|`DBTYPE_UI4`||描述參數特性的位元遮罩：<br /><br /> -   `DM_PARAMETER_TRAINING` (`0x0000001`) 指出參數用於訓練<br />-   `DM_PARAMETER_PREDICTION` (`0x00000002`) 指出參數用來預測<br />-   `DM_PARAMETER_CONTENT` (`0x00000003`) 指出參數用於內容限制|  
|`DESCRIPTION`|`DBTYPE_WSTR`||使用者易記的參數描述。|  
|`DEFAULT_VALUE`|`DBTYPE_WSTR`||參數的預設值。 如果預設值不是簡單的資料類型，會傳回 `NULL`。|  
|`VALUE_ENUMERATION`|`DBTYPE_WSTR`||參數的可能值之列舉值。|  
|`HELP_FILE`|`DBTYPE_WSTR`||包含此參數文件集的檔案名稱。|  
|`HELP_CONTEXT`|`DBTYPE_I4`||這個函數的說明內容識別碼。|  
  
## <a name="restriction-columns"></a>限制資料行  
 在下表列出的資料行上可能會限制 `DMSCHEMA_MINING_SERVICE_PARAMETERS` 資料列集。  
  
|資料行名稱|類型指標|限制狀態|  
|-----------------|--------------------|-----------------------|  
|`SERVICE_NAME`|`DBTYPE_WSTR`|選擇性。|  
|`PARAMETER_NAME`|`DBTYPE_WSTR`|選擇性。|  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦結構描述資料列集](../../schema-rowsets/data-mining/data-mining-schema-rowsets.md) 
  
  
