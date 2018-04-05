---
title: DMSCHEMA_MINING_SERVICE_PARAMETERS 資料列集 |Microsoft 文件
ms.custom: ''
ms.date: 03/03/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- DMSCHEMA_MINING_SERVICE_PARAMETERS
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DMSCHEMA_MINING_SERVICE_PARAMETERS rowset
ms.assetid: 5994e66b-84d0-4279-9f50-d92fd829dd83
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 497396bf0679afbabbebe9936ba6c5f443942bec
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="dmschemaminingserviceparameters-rowset"></a>DMSCHEMA_MINING_SERVICE_PARAMETERS 資料列集
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]描述演算法的參數在伺服器上。  
  
## <a name="rowset-columns"></a>資料列集資料行  
 **DMSCHEMA_MINING_SERVICE_PARAMETERS**資料列集包含下列資料行。  
  
|資料行名稱|類型指標|描述|  
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
  
## <a name="see-also"></a>請參閱  
 [資料採礦結構描述資料列集](../../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)  
  
  
