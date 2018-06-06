---
title: DMSCHEMA_MINING_SERVICE_PARAMETERS 資料列集 |Microsoft 文件
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 41554600e77c3055f998d7fa32b6f7330c06de52
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="dmschemaminingserviceparameters-rowset"></a>DMSCHEMA_MINING_SERVICE_PARAMETERS 資料列集
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  描述伺服器上演算法的參數。  
  
## <a name="rowset-columns"></a>資料列集資料行  
 **DMSCHEMA_MINING_SERVICE_PARAMETERS**資料列集包含下列資料行。  
  
|資料行名稱|類型指標|Description|  
|-----------------|--------------------|-----------------|  
|**服務名稱**|**DBTYPE_WSTR**|演算法的名稱。|  
|**PARAMETER_NAME**|**DBTYPE_WSTR**|參數的名稱。|  
|**P**|**DBTYPE_WSTR**|參數的類型。|  
|**IS_REQUIRED**|**DBTYPE_BOOL**|布林值，傳回**TRUE**如果參數是必要項。|  
|**PARAMETER_FLAGS**|**DBTYPE_UI4**|描述參數特性的位元遮罩：<br /><br /> **DM_PARAMETER_TRAINING** (**0x0000001**) 指出參數用於訓練<br /><br /> **DM_PARAMETER_PREDICTION** (**0x00000002**) 指出參數用於預測<br /><br /> **DM_PARAMETER_CONTENT** (**0x00000003**) 指出參數用於內容限制|  
|**DESCRIPTION**|**DBTYPE_WSTR**|使用者易記的參數描述。|  
|**預設值**|**DBTYPE_WSTR**|參數的預設值。 傳回**NULL**如果預設值不是簡單的資料類型。|  
|**VALUE_ENUMERATION**|**DBTYPE_WSTR**|參數的可能值之列舉值。|  
|**HELP_FILE**|**DBTYPE_WSTR**|包含此參數文件集的檔案名稱。|  
|**HELP_CONTEXT**|**DBTYPE_I4**|這個函數的說明內容識別碼。|  
  
## <a name="restriction-columns"></a>限制資料行  
 **DMSCHEMA_MINING_SERVICE_PARAMETERS**上表中列出的資料行可能會限制資料列集。  
  
|資料行名稱|類型指標|限制狀態|  
|-----------------|--------------------|-----------------------|  
|**服務名稱**|**DBTYPE_WSTR**|選擇性。|  
|**PARAMETER_NAME**|**DBTYPE_WSTR**|選擇性。|  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦結構描述資料列集](../../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)  
  
  
