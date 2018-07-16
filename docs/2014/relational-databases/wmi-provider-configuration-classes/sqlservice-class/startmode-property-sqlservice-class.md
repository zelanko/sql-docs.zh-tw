---
title: StartMode 屬性 （SqlService 類別） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- StartMode Property (SqlService Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- StartMode property
ms.assetid: c0c2c7f8-d4ae-44f2-ad8e-aecfcb7c2878
caps.latest.revision: 36
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: c3bed01976385885d84768101d8b64c9436fdcea
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37307488"
---
# <a name="startmode-property-sqlservice-class"></a>StartMode 屬性 (SqlService 類別)
  取得服務的啟動模式。  
  
## <a name="syntax"></a>語法  
  
```  
  
object  
.StartMode [= value]  
```  
  
## <a name="parts"></a>組件  
 *object*  
 表示此服務的 [SqlService 類別](sqlservice-class.md) 物件。  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 指定服務模式的 uint32 值。  
  
 它可以是下列其中一個值。  
  
 Boot  
 值 = 0。 由作業系統載入程式啟動的服務。 這個選項只對驅動程式服務有效。  
  
 系統  
 值 = 1。 由 `IoInitSystem` 方法啟動的服務。 這個選項只對驅動程式服務有效。  
  
 自動  
 值 = 2。 要由服務控制管理員在系統啟動期間自動啟動的服務。  
  
 手動  
 值 = 3。 在處理序呼叫 `StartService` 方法時要由電腦管理員啟動的服務。  
  
 已停用  
 值 = 4。 無法啟動服務。  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [啟動及停止服務](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
