---
description: ErrorControl 屬性 (SqlService 類別)
title: 'ErrorControl 屬性 (SqlService) '
ms.custom: seo-lt-2019
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- ErrorControl Property (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- ErrorControl property
ms.assetid: cbb1e0fa-5bfc-4b1b-a6ed-f7d5cfad4d73
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 47b62734773d7b3e4f027d0e31671f65a66ae9a9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88427200"
---
# <a name="errorcontrol-property-sqlservice-class"></a>ErrorControl 屬性 (SqlService 類別)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  當服務在啟動期間無法啟動時，取得或設定錯誤的嚴重性。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.ErrorControl [= value]  
```  
  
## <a name="parts"></a>組件  
 *object*  
 表示此服務的 [SqlService 類別](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) 物件。  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 字串值，可指定當服務在啟動期間失敗時所報告的錯誤嚴重性。 下表顯示可能的值。  
  
 忽略  
 不通知使用者。  
  
 正常  
 通知使用者。  
  
 Severe  
 使用上次的正確組態重新啟動系統。  
  
 重大  
 系統嘗試以正確的組態重新啟動。  
  
 Unknown  
 嚴重性未知。  
  
## <a name="remarks"></a>備註  
 此值表示在發生失敗時由啟動程式採取的動作。 電腦系統會記錄所有錯誤。  
  
## <a name="see-also"></a>另請參閱  
 [啟動及停止服務](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
