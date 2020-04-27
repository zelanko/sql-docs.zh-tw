---
title: SetBoolValue 方法（SqlServiceAdvancedProperty 類別） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
api_name:
- SetBoolValue Method (SqlServiceAdvancedProperty Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- SetBoolValue method
ms.assetid: 5252b439-fce5-446a-8e57-99e3054bee69
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 302ac36150d21dfecca1e6c6edfbcf6fd86c42f0
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "63226145"
---
# <a name="setboolvalue-method-sqlserviceadvancedproperty-class"></a>SetBoolValue 方法 (SqlServiceAdvancedProperty 類別)
  設定屬性的布林值。  
  
## <a name="syntax"></a>語法  
  
```  
  
object  
.SetBoolValue [= value]  
```  
  
## <a name="parts"></a>組件  
 *物件*  
 代表進階屬性的 [SqlServiceAdvancedProperty 類別](../wmi-provider-configuration-classes/sqlserviceadvancedproperty-class/sqlserviceadvancedproperty-class.md) 物件。  
  
#### <a name="parameters"></a>參數  
  
|參數|描述|  
|---------------|-----------------|  
|*BoolValue*|指定進階屬性值的布林值。|  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 `uint32` 值，如果已成功修改此服務為 0，如果不支援要求則為 1，以及其他指示錯誤的任何數字。  
  
## <a name="remarks"></a>備註  
 屬性值類型必須是布林，才能將屬性設定為布林值。  
  
## <a name="see-also"></a>另請參閱  
 [啟動及停止服務](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
