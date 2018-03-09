---
title: "ErrorControl 屬性 （SqlService 類別） |Microsoft 文件"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: wmi
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- ErrorControl Property (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- ErrorControl property
ms.assetid: cbb1e0fa-5bfc-4b1b-a6ed-f7d5cfad4d73
caps.latest.revision: 
author: JennieHubbard
ms.author: jhubbard
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2e0ad1c02cf0444431c583f3f7d06016fd9502c8
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/12/2018
---
# <a name="errorcontrol-property-sqlservice-class"></a>ErrorControl 屬性 (SqlService 類別)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
當服務在啟動期間無法啟動時，取得或設定錯誤的嚴重性。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.ErrorControl [= value]  
```  
  
## <a name="parts"></a>組件  
 *物件*  
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
 [啟動及停止服務](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
