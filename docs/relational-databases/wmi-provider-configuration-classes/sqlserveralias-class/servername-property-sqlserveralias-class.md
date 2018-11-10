---
title: ServerName 屬性 （SqlServerAlias 類別） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- ServerName Property (SqlServerAlias Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- ServerName property
ms.assetid: 58c82b19-b548-42fa-9c5a-059b606da097
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 4d65c718dbf92e75e9d5c21f872ae77240710fa9
ms.sourcegitcommit: 6c9d35d03c1c349bc82b9ed0878041d976b703c6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/06/2018
ms.locfileid: "51217786"
---
# <a name="servername-property-sqlserveralias-class"></a>ServerName 屬性 (SqlServerAlias 類別)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  取得執行個體名稱[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]伺服器連接別名所指定。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.ServerName [= value]  
```  
  
## <a name="parts"></a>組件  
 *object*  
 A [SqlServerAlias 類別](../../../relational-databases/wmi-provider-configuration-classes/sqlserveralias-class/sqlserveralias-class.md)物件，表示[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]別名。  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 指定由伺服器連接別名所參考之 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體名稱的字串值。  
  
## <a name="remarks"></a>備註  
  
