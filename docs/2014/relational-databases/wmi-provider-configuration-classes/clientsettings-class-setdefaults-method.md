---
title: SetDefaults 方法 （ClientSettings 類別） |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- SetDefaults Method (ClientSettings Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- SetDefaults method
ms.assetid: 056508f3-a5c8-467c-a196-dc1ef1f5178f
caps.latest.revision: 28
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 58cfbe5b2a53bfdce97037602058466ccd1af187
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36133669"
---
# <a name="setdefaults-method-clientsettings-class"></a>SetDefaults 方法 (ClientSettings 類別)
  設定執行個體的所有預設值[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]選項來覆寫現有資料的用戶端。  
  
## <a name="syntax"></a>語法  
  
```  
  
object  
.SetDefaults(  
OverwriteAll  
)  
  
```  
  
## <a name="parts"></a>組件  
 *object*  
 代表 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用戶端執行個體的 `ClientSettings` 物件。  
  
#### <a name="parameters"></a>參數  
  
|參數|描述|  
|---------------|-----------------|  
|*OverwriteAll*|指定是否要覆寫 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用戶端執行個體上之現有值的布林值。 `true` 表示要覆寫現有的資料，`false` 表示不覆寫現有的資料。|  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 `uint32` 值，如果已成功修改此服務為 0，如果不支援要求則為 1，以及其他指示錯誤的任何數字。  
  
## <a name="remarks"></a>備註  
  