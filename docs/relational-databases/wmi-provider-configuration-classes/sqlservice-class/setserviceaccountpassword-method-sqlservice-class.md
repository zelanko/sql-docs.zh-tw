---
title: SetServiceAccountPassword 方法 （SqlService 類別） |Microsoft 文件
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: wmi
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- SetServiceAccountPassword Method (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetServiceAccountPassword method
ms.assetid: e577a1ac-985c-4799-bb38-9393efc3def2
caps.latest.revision: 36
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 07b3db70f8f4a4bb50c3c613501feebf7296f58e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="setserviceaccountpassword-method-sqlservice-class"></a>SetServiceAccountPassword 方法 (SqlService 類別)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  修改參考之服務執行時所使用之帳戶的密碼。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.SetServiceAccountPassword(AccountOldPassword , ServiceStartPassword)  
```  
  
## <a name="parts"></a>組件  
 *物件*  
 表示此服務的 [SqlService 類別](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) 物件。  
  
#### <a name="parameters"></a>參數  
 *AccountOldPassword*  
 指定帳戶之現有密碼的字串值。  
  
 *ServiceStartPassword*  
 指定帳戶之新密碼的字串值。  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 A **uint32**值為 0，如果已成功修改此服務，不支援要求，則為 1，而其他數值則表示錯誤。  
  
## <a name="remarks"></a>備註  
  
