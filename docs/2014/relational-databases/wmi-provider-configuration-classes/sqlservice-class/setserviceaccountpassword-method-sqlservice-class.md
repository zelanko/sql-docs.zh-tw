---
title: SetServiceAccountPassword 方法（SqlService 類別） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- SetServiceAccountPassword Method (SqlService Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- SetServiceAccountPassword method
ms.assetid: e577a1ac-985c-4799-bb38-9393efc3def2
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 41823ebcbad3f545a8b516b3fad457230d3fdf8e
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85067874"
---
# <a name="setserviceaccountpassword-method-sqlservice-class"></a>SetServiceAccountPassword 方法 (SqlService 類別)
  修改參考之服務執行時所使用之帳戶的密碼。  
  
## <a name="syntax"></a>語法  
  
```  
  
object  
.SetServiceAccountPassword(  
AccountOldPassword , ServiceStartPassword  
)  
  
```  
  
## <a name="parts"></a>組件  
 *object*  
 表示此服務的 [SqlService 類別](sqlservice-class.md) 物件。  
  
#### <a name="parameters"></a>參數  
 *AccountOldPassword*  
 指定帳戶之現有密碼的字串值。  
  
 *ServiceStartPassword*  
 指定帳戶之新密碼的字串值。  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 `uint32` 值，如果已成功修改此服務為 0，如果不支援要求則為 1，以及其他指示錯誤的任何數字。  
  
## <a name="remarks"></a>備註  
  
