---
title: SetStartMode 方法（SqlService）
ms.custom: seo-lt-2019
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
ms.openlocfilehash: edd3b4a5fa4d787292f1978da80c5f7803242010
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/06/2019
ms.locfileid: "73660905"
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
 指定服務實例之啟動模式的**uint32**值。  
  
 有效值如下：  
  
 值 = 0。 Boot - 由作業系統載入程式啟動的裝置驅動程式。 這個值只適用於驅動程式服務。  
  
 值 = 1。 由**IoInitSystem**方法啟動的系統裝置磁碟機。 這個值只適用於驅動程式服務。  
  
 值 = 2。 Automatic - 要由服務控制管理員在系統啟動期間自動啟動的服務。  
  
 值 = 3。 Manual-當進程呼叫**StartService**方法時，由電腦系統管理員啟動的服務。  
  
 值 = 4。 Disabled - 無法再啟動服務。  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 **Uint32**值，如果已成功修改服務，則為0，如果不支援要求則為1。 任何其他數字表示發生錯誤。  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [啟動和停止服務](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
