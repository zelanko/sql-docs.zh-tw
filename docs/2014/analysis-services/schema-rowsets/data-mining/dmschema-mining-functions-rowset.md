---
title: DMSCHEMA_MINING_FUNCTIONS 資料列集 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- DMSCHEMA_MINING_FUNCTIONS
topic_type:
- apiref
helpviewer_keywords:
- DMSCHEMA_MINING_FUNCTIONS rowset
ms.assetid: 9ace7493-a7b1-45ca-93de-3cb2f3597017
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b769476650bdb97479f3d8c61871980605e75635
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48190414"
---
# <a name="dmschemaminingfunctions-rowset"></a>DMSCHEMA_MINING_FUNCTIONS 資料列集
  描述正在執行的伺服器上可用的資料採礦演算法所支援的資料採礦功能[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
## <a name="rowset-columns"></a>資料列集資料行  
 `DMSCHEMA_MINING_FUNCTIONS`資料列集包含下列資料行。  
  
|資料行名稱|類型指標|長度|描述|  
|-----------------|--------------------|------------|-----------------|  
|`SERVICE_NAME`|`DBTYPE_WSTR`||演算法的名稱。|  
|`FUNCTION_NAME`|`DBTYPE_WSTR`||函數的名稱。|  
|`FUNCTION_SIGNATURE`|`DBTYPE_WSTR`||函數的簽名。|  
|`RETURNS_TABLE`|`DBTYPE_BOOL`||如果函數傳回純量內容 (例如字元引數的長度)，則為 `FALSE`；如果函數傳回資料表 (例如，長條圖資料表)，則為 `TRUE`。|  
|`DESCRIPTION`|`DBTYPE_WSTR`||使用者易記的函數描述。|  
|`HELP_FILE`|`DBTYPE_WSTR`||包含此函數文件集的檔案名稱。|  
|`HELP_CONTEXT`|`DBTYPE_I4`||這個函數的說明內容識別碼。|  
  
## <a name="restriction-columns"></a>限制資料行  
 在下表列出的資料行上可能會限制 `DMSCHEMA_MINING_FUNCTIONS` 資料列集。  
  
|資料行名稱|類型指標|限制狀態|  
|-----------------|--------------------|-----------------------|  
|`SERVICE_NAME`|`DBTYPE_WSTR`|選擇性。|  
|`FUNCTION_NAME`|`DBTYPE_WSTR`|選擇性。|  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦結構描述資料列集](../../schema-rowsets/data-mining/data-mining-schema-rowsets.md) 
  
  
