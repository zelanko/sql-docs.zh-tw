---
title: ErrorControl 屬性 （SqlService 類別） |Microsoft Docs
ms.custom: ''
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
manager: craigg
ms.openlocfilehash: 5840300e97328e3b9d203e2c74aeec0dba06d068
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/15/2018
ms.locfileid: "51656667"
---
# <a name="errorcontrol-property-sqlservice-class"></a>ErrorControl 屬性 (SqlService 類別)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
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
  
 Ignore  
 不通知使用者。  
  
 一般  
 通知使用者。  
  
 Severe  
 使用上次的正確組態重新啟動系統。  
  
 嚴重  
 系統嘗試以正確的組態重新啟動。  
  
 Unknown  
 嚴重性未知。  
  
## <a name="remarks"></a>備註  
 此值表示在發生失敗時由啟動程式採取的動作。 電腦系統會記錄所有錯誤。  
  
## <a name="see-also"></a>另請參閱  
 [啟動及停止服務](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
