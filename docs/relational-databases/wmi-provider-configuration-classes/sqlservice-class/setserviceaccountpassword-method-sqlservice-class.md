---
title: SetServiceAccountPassword 方法 （SqlService 類別） |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SetServiceAccountPassword Method (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetServiceAccountPassword method
ms.assetid: e577a1ac-985c-4799-bb38-9393efc3def2
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: ead4a08e653c1898a183b808ad85a3709c14370f
ms.sourcegitcommit: 6c9d35d03c1c349bc82b9ed0878041d976b703c6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/06/2018
ms.locfileid: "51217596"
---
# <a name="setserviceaccountpassword-method-sqlservice-class"></a>SetServiceAccountPassword 方法 (SqlService 類別)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  修改參考之服務執行時所使用之帳戶的密碼。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.SetServiceAccountPassword(AccountOldPassword , ServiceStartPassword)  
```  
  
## <a name="parts"></a>組件  
 *object*  
 表示此服務的 [SqlService 類別](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) 物件。  
  
#### <a name="parameters"></a>參數  
 *AccountOldPassword*  
 指定帳戶之現有密碼的字串值。  
  
 *ServiceStartPassword*  
 指定帳戶之新密碼的字串值。  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 A **uint32**值，也就是 0，如果已成功修改此服務，不支援要求，則為 1，而其他數值則表示錯誤。  
  
## <a name="remarks"></a>備註  
  
