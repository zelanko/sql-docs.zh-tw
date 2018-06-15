---
title: SetStartMode 方法 （SqlService 類別） |Microsoft 文件
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: wmi
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- SetStartMode Method (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetStartMode method
ms.assetid: f6f198b4-f9a4-468c-8977-76462ef06e61
caps.latest.revision: 35
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 5f3973183d5564f813ab12c561e7097b3f68f09d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "33010135"
---
# <a name="setstartmode-method-sqlservice-class"></a>SetStartMode 方法 (SqlService 類別)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  修改服務執行個體的啟動模式。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.SetStartMode(StartMode)  
```  
  
## <a name="parts"></a>組件  
 *物件*  
 表示此服務的 [SqlService 類別](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) 物件。  
  
#### <a name="parameters"></a>參數  
 *StartMode*  
 A **uint32**值，指定服務執行個體的啟動模式。  
  
 有效值如下：  
  
 值 = 0。 Boot - 由作業系統載入程式啟動的裝置驅動程式。 這個值只適用於驅動程式服務。  
  
 值 = 1。 系統-開始裝置驅動程式**IoInitSystem**方法。 這個值只適用於驅動程式服務。  
  
 值 = 2。 Automatic - 要由服務控制管理員在系統啟動期間自動啟動的服務。  
  
 值 = 3。 Manual-服務在啟動處理程序呼叫時由電腦管理員**StartService**方法。  
  
 值 = 4。 Disabled - 無法再啟動服務。  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 A **uint32**值，如果成功修改此服務為 0 或 1，表示不支援要求。 任何其他數字表示發生錯誤。  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [啟動及停止服務](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
