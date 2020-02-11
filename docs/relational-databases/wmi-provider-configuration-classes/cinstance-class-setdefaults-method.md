---
title: SetDefaults 方法（CInstance）
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SetDefaults Method (CInstance Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetDefaults method
ms.assetid: ed9e99c2-3e28-4ee8-bc20-61ca05984973
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: d75a202b368df339b97a4a9588ad3ac073429c6e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "73659635"
---
# <a name="cinstance-class---setdefaults-method"></a>CInstance 類別 - SetDefaults 方法
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  使用覆寫現有資料的選項，設定[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用戶端實例的所有預設值。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.SetDefaults(OverwriteAll)  
```  
  
## <a name="parts"></a>組件  
 *目標*  
 代表 [用戶端執行個體的](../../relational-databases/wmi-provider-configuration-classes/cinstance-class.md) CInstance 類別 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 物件。  
  
#### <a name="parameters"></a>參數  
  
|參數|描述|  
|---------------|-----------------|  
|*OverwriteAll*|布林值，指定是否要覆寫[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用戶端實例上現有的值： **true**表示要覆寫現有的資料，如果不覆寫現有的資料，則為**false** 。|  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 **Uint32**值，如果已成功修改服務，則為0，如果不支援要求則為1，以及其他指示錯誤的任何數位。  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [設定用戶端通訊協定](https://technet.microsoft.com/library/ms181035.aspx)  
  
  
