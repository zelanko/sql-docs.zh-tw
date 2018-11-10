---
title: ConnectionString 屬性 （SqlServerAlias 類別） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- ConnectionString Property (SqlServerAlias Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
helpviewer_keywords:
- ConnectionString property
ms.assetid: 8a3692b9-3a34-42e2-b0b9-28e6bd3a7aba
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: c2c1ef8d472e20d8fb8148050286b09405a10fd0
ms.sourcegitcommit: 6c9d35d03c1c349bc82b9ed0878041d976b703c6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/06/2018
ms.locfileid: "51217516"
---
# <a name="connectionstring-property-sqlserveralias-class"></a>ConnectionString 屬性 (SqlServerAlias 類別)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  取得用來為伺服器連接別名建立連接的連接字串。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.ConnectionString [= value]  
```  
  
## <a name="parts"></a>組件  
 *object*  
 A [SqlServerAlias 類別](../../../relational-databases/wmi-provider-configuration-classes/sqlserveralias-class/sqlserveralias-class.md)物件，表示[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]別名。  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 一個字串，可指定用來為伺服器連接別名建立連接的連接字串。  
  
## <a name="remarks"></a>備註  
  
