---
title: SetDefaults 方法（ClientSettings）
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SetDefaults Method (ClientSettings Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetDefaults method
ms.assetid: 056508f3-a5c8-467c-a196-dc1ef1f5178f
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: fd88ef9b93dd20a7cf77e70dddb8a2733ee5a4ea
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85888863"
---
# <a name="clientsettings-class---setdefaults-method"></a>ClientSettings 類別 - SetDefaults 方法
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用覆寫現有資料的選項，設定用戶端實例的所有預設值。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.SetDefaults(OverwriteAll)  
```  
  
## <a name="parts"></a>組件  
 *object*  
 代表**ClientSettings** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用戶端實例的 ClientSettings 物件。  
  
#### <a name="parameters"></a>參數  
  
|參數|說明|  
|---------------|-----------------|  
|*OverwriteAll*|指定是否要覆寫 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用戶端執行個體上之現有值的布林值。 **true**表示覆寫現有的資料;如果不覆寫現有的資料，則**為 false** 。|  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 **Uint32**值，如果已成功修改服務，則為0，如果不支援要求則為1，以及其他指示錯誤的任何數位。  
  
## <a name="remarks"></a>備註  
  
