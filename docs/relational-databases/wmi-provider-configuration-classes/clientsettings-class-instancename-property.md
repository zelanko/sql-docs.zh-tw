---
title: InstanceName 屬性 （ClientSettings 類別） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: reference
apiname:
- InstanceName Property (ClientSettings Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- InstanceName property
ms.assetid: 58dacb4a-751a-491f-9adb-88ec6afc797c
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: e587c7a087c2a93ef4a697c5d17d8bc0a61b7155
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47694026"
---
# <a name="clientsettings-class---instancename-property"></a>ClientSettings 類別 - InstanceName 屬性
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  取得 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用戶端的執行個體名稱。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.InstanceName [= value]  
```  
  
## <a name="parts"></a>組件  
 *object*  
 A **ClientSettings**物件，表示設定上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用戶端執行個體。  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用戶端執行個體名稱的字串值。  
  
## <a name="remarks"></a>備註  
  
