---
title: SetDefaults 方法 （ServerSettings 類別） |Microsoft Docs
ms.custom: ''
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
ms.openlocfilehash: 094406b6bd8a07123049837318c00238ffaa2b84
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68052807"
---
# <a name="setdefaults-method-serversettings-class"></a>SetDefaults 方法 (ServerSettings 類別)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  設定執行個體的所有預設值[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]覆寫現有資料的選項。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.SetDefaults(OverwriteAll)  
```  
  
## <a name="parts"></a>組件  
 *object*  
 A [ServerSettings 類別](../../../relational-databases/wmi-provider-configuration-classes/serversettings-class/serversettings-class.md)物件，表示[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]用戶端執行個體。  
  
#### <a name="parameters"></a>參數  
  
|參數|描述|  
|---------------|-----------------|  
|*OverwriteAll*|布林值，指定是否要覆寫現有值執行個體上的[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: **，則為 true**覆寫現有的資料，或**false**則現有資料不會覆寫。|  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 u**int32** 值，如果已成功修改此服務為 0，如果不支援要求則為 1，以及其他指示錯誤的任何數字。  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [設定伺服器網路通訊協定和網路程式庫](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
