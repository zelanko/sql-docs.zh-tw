---
title: SetDefaults 方法 （SInstance 類別） |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
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
- SetDefaults Method (SInstance Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetDefaults method
ms.assetid: dc3c6a85-0711-4688-bf4f-91168c57af28
caps.latest.revision: 30
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 50f735e7d41d4a77f2d99aa11bf92b474a033629
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="setdefaults-method-sinstance-class"></a>SetDefaults 方法 (SInstance 類別)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  設定執行個體的所有預設值[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]覆寫現有資料的選項。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.SetDefaults(OverwriteAll)  
```  
  
## <a name="parts"></a>組件  
 *物件*  
 [SInstance 類別](../../../relational-databases/wmi-provider-configuration-classes/sinstance-class/sinstance-class.md)物件，表示伺服器執行個體。  
  
#### <a name="parameters"></a>參數  
  
|매개 변수|Description|  
|---------------|-----------------|  
|*OverwriteAll*|布林值，指定是否要覆寫的執行個體上的現有值[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]用戶端： **true**如果覆寫現有的資料，或**false**如果現有的資料不會覆寫。|  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 A **uint32**值為 0，如果已成功修改此服務，不支援要求，則為 1，而其他數值則表示錯誤。  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [設定伺服器網路通訊協定和網路程式庫](http://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
