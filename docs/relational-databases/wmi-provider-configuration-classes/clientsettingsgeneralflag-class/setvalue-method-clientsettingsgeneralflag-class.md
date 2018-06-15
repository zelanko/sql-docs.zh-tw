---
title: SetValue 方法 （ClientSettingsGeneralFlag 類別） |Microsoft 文件
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
- SetValue Method (ClientSettingsGeneralFlag Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetValue method
ms.assetid: 34443689-a0e0-4668-a811-17532c6fd271
caps.latest.revision: 14
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 726e32390d58a9b1c3e1f80e2fca5b958b41fae5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "33008925"
---
# <a name="setvalue-method-clientsettingsgeneralflag-class"></a>SetValue 方法 (ClientSettingsGeneralFlag 類別)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  設定參考之旗標的所有值。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.SetValue(Value)  
```  
  
## <a name="parts"></a>組件  
 *物件*  
 表示伺服器設定之一般旗標的 [ClientSettingsGeneralFlag 類別](../../../relational-databases/wmi-provider-configuration-classes/clientsettingsgeneralflag-class/clientsettingsgeneralflag-class.md) 物件。  
  
#### <a name="parameters"></a>參數  
  
|매개 변수|Description|  
|---------------|-----------------|  
|*值*|指定旗標之值的布林值。|  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 A **uint32**值為 0，如果已成功修改此服務，不支援要求，則為 1，而其他數值則表示錯誤。  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [設定用戶端通訊協定](http://technet.microsoft.com/library/ms181035.aspx)  
  
  
