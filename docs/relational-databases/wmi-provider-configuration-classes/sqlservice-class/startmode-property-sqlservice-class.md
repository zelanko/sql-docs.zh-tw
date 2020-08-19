---
description: StartMode 屬性 (SqlService 類別)
title: 'StartMode 屬性 (SqlService) '
ms.custom: seo-lt-2019
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- StartMode Property (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- StartMode property
ms.assetid: c0c2c7f8-d4ae-44f2-ad8e-aecfcb7c2878
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 608214cf9d4eca2601c0f8bee7b82570ec936ea6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88418754"
---
# <a name="startmode-property-sqlservice-class"></a>StartMode 屬性 (SqlService 類別)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  取得服務的啟動模式。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.StartMode [= value]  
```  
  
## <a name="parts"></a>組件  
 *object*  
 表示此服務的 [SqlService 類別](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) 物件。  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 指定服務模式的 uint32 值。  
  
 它可以是下列其中一個值。  
  
 Boot  
 值 = 0。 由作業系統載入程式啟動的服務。 這個選項只對驅動程式服務有效。  
  
 系統  
 值 = 1。 **IoInitSystem**方法啟動的服務。 這個選項只對驅動程式服務有效。  
  
 自動  
 值 = 2。 要由服務控制管理員在系統啟動期間自動啟動的服務。  
  
 手動  
 值 = 3。 當進程呼叫 **StartService** 方法時，由電腦系統管理員啟動的服務。  
  
 已停用  
 值 = 4。 無法啟動服務。  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [啟動及停止服務](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
