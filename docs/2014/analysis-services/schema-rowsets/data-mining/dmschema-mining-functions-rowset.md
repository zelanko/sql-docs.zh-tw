---
title: DMSCHEMA_MINING_FUNCTIONS 資料列集 |Microsoft 文件
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
- DMSCHEMA_MINING_FUNCTIONS
topic_type:
- apiref
helpviewer_keywords:
- DMSCHEMA_MINING_FUNCTIONS rowset
ms.assetid: 9ace7493-a7b1-45ca-93de-3cb2f3597017
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: b5a60e18a57c15976e7a7bd5d5e31729e255869a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36136509"
---
# <a name="dmschemaminingfunctions-rowset"></a>DMSCHEMA_MINING_FUNCTIONS 資料列集
  描述可在伺服器上執行資料採礦演算法所支援之資料採礦函數[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
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
  
  