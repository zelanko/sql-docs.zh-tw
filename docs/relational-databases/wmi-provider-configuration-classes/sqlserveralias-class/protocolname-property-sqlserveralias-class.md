---
title: ProtocolName 屬性 （SqlServerAlias 類別） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: reference
apiname:
- ProtocolName Property (SqlServerAlias Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- ProtocolName property
ms.assetid: 8fb81ab3-15f1-4a71-be72-2072c6bcc670
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 0e9cdf0d7113bbd02b379431f152367de8d78281
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47601297"
---
# <a name="protocolname-property-sqlserveralias-class"></a>ProtocolName 屬性 (SqlServerAlias 類別)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  取得伺服器連接別名所使用的通訊協定名稱。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.ProtocolName [= value]  
```  
  
## <a name="parts"></a>組件  
 *object*  
 A [SqlServerAlias 類別](../../../relational-databases/wmi-provider-configuration-classes/sqlserveralias-class/sqlserveralias-class.md)物件，表示[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]別名。  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 指定由伺服器連接別名所使用之通訊協定名稱的字串值。  
  
## <a name="remarks"></a>備註  
  
