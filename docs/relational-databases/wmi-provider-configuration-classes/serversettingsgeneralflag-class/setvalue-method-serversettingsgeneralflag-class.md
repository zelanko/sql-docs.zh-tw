---
title: "SetValue 方法 （ServerSettingsGeneralFlag 類別） |Microsoft 文件"
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
- SetValue Method (ServerSettingsGeneralFlag Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetValue method
ms.assetid: a889feac-c0e0-4635-b506-843863d86967
caps.latest.revision: 
author: JennieHubbard
ms.author: jhubbard
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ca4811fd144dc27ab244e42e75a30ff86f6cd1d7
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/12/2018
---
# <a name="setvalue-method-serversettingsgeneralflag-class"></a>SetValue 方法 (ServerSettingsGeneralFlag 類別)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
設定參考之旗標的所有值。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.SetValue(Value)  
```  
  
## <a name="parts"></a>組件  
 *物件*  
 表示伺服器設定之一般旗標的 [ServerSettingsGeneralFlag 類別](../../../relational-databases/wmi-provider-configuration-classes/serversettingsgeneralflag-class/serversettingsgeneralflag-class.md) 物件。  
  
#### <a name="parameters"></a>參數  
  
|매개 변수|Description|  
|---------------|-----------------|  
|*值*|指定旗標之值的布林值。|  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 A **uint32**值為 0，如果已成功修改此服務，不支援要求，則為 1，而其他數值則表示錯誤。  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [設定伺服器網路通訊協定和網路程式庫](http://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
