---
title: SetDefaults 方法（ServerSettings）
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SetDefaults Method (ServerSettings Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetDefaults method
ms.assetid: 76e4cfab-4b15-4da4-bb2f-8aac6f927f79
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 86e15376bd56a439e0763e79a5c166d7023125ea
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/06/2019
ms.locfileid: "73660266"
---
# <a name="setdefaults-method-serversettings-class"></a>SetDefaults 方法 (ServerSettings 類別)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  使用覆寫現有資料的選項，設定 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 實例的所有預設值。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.SetDefaults(OverwriteAll)  
```  
  
## <a name="parts"></a>組件  
 *object*  
 代表 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 用戶端實例的[ServerSettings 類別](../../../relational-databases/wmi-provider-configuration-classes/serversettings-class/serversettings-class.md)物件。  
  
#### <a name="parameters"></a>參數  
  
|參數|說明|  
|---------------|-----------------|  
|*OverwriteAll*|布林值，指定是否要覆寫 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]的實例上現有的值： **true**以覆寫現有的資料，如果不覆寫現有的資料，則為**false** 。|  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 u**int32** 值，如果已成功修改此服務為 0，如果不支援要求則為 1，以及其他指示錯誤的任何數字。  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [設定伺服器網路通訊協定和網路程式庫](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
