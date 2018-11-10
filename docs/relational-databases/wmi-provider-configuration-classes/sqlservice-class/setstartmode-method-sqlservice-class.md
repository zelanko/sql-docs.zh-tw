---
title: SetStartMode 方法 （SqlService 類別） |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SetStartMode Method (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetStartMode method
ms.assetid: f6f198b4-f9a4-468c-8977-76462ef06e61
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 9d1720bc8aba384b4a3b10969abbcc4cfb5cf3fc
ms.sourcegitcommit: 6c9d35d03c1c349bc82b9ed0878041d976b703c6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/06/2018
ms.locfileid: "51217456"
---
# <a name="setstartmode-method-sqlservice-class"></a>SetStartMode 方法 (SqlService 類別)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  修改服務執行個體的啟動模式。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.SetStartMode(StartMode)  
```  
  
## <a name="parts"></a>組件  
 *object*  
 表示此服務的 [SqlService 類別](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) 物件。  
  
#### <a name="parameters"></a>參數  
 *StartMode*  
 A **uint32**值，指定服務執行個體的啟動模式。  
  
 有效值如下：  
  
 值 = 0。 Boot - 由作業系統載入程式啟動的裝置驅動程式。 這個值只適用於驅動程式服務。  
  
 值 = 1。 系統-裝置驅動程式開始著手**IoInitSystem**方法。 這個值只適用於驅動程式服務。  
  
 值 = 2。 Automatic - 要由服務控制管理員在系統啟動期間自動啟動的服務。  
  
 值 = 3。 手動-要啟動由電腦管理員，當處理程序呼叫的服務**StartService**方法。  
  
 值 = 4。 Disabled - 無法再啟動服務。  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 A **uint32**值，則為 0，如果成功修改此服務或不支援要求，則為 1。 任何其他數字表示發生錯誤。  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [啟動及停止服務](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
