---
title: DMSCHEMA_MINING_FUNCTIONS 資料列集 |Microsoft 文件
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f92a3028f9397283f8d5820c54d823e40b8fdc3d
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="dmschemaminingfunctions-rowset"></a>DMSCHEMA_MINING_FUNCTIONS 資料列集
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  描述可在伺服器上執行資料採礦演算法所支援之資料採礦函數[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
## <a name="rowset-columns"></a>資料列集資料行  
 **DMSCHEMA_MINING_FUNCTIONS**資料列集包含下列資料行。  
  
|資料行名稱|類型指標|長度|Description|  
|-----------------|--------------------|------------|-----------------|  
|**服務名稱**|**DBTYPE_WSTR**||演算法的名稱。|  
|**FUNCTION_NAME**|**DBTYPE_WSTR**||函數的名稱。|  
|**FUNCTION_SIGNATURE**|**DBTYPE_WSTR**||函數的簽名。|  
|**RETURNS_TABLE**|**DBTYPE_BOOL**||**FALSE**如果函數傳回純量內容 （例如字元引數的長度）;**TRUE**如果函數傳回的資料表 （例如，長條圖資料表）。|  
|**DESCRIPTION**|**DBTYPE_WSTR**||使用者易記的函數描述。|  
|**HELP_FILE**|**DBTYPE_WSTR**||包含此函數文件集的檔案名稱。|  
|**HELP_CONTEXT**|**DBTYPE_I4**||這個函數的說明內容識別碼。|  
  
## <a name="restriction-columns"></a>限制資料行  
 **DMSCHEMA_MINING_FUNCTIONS**上表中列出的資料行可能會限制資料列集。  
  
|資料行名稱|類型指標|限制狀態|  
|-----------------|--------------------|-----------------------|  
|**服務名稱**|**DBTYPE_WSTR**|選擇性。|  
|**FUNCTION_NAME**|**DBTYPE_WSTR**|選擇性。|  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦結構描述資料列集](../../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)  
  
  
