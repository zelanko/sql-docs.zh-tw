---
title: "ConnectionString 屬性 （SqlServerAlias 類別） |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: wmi
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname: ConnectionString Property (SqlServerAlias Class)
apilocation: sqlmgmproviderxpsp2up.mof
helpviewer_keywords: ConnectionString property
ms.assetid: 8a3692b9-3a34-42e2-b0b9-28e6bd3a7aba
caps.latest.revision: "30"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 674966101fe0b0290f4cb95dcf8353e5c6228ac5
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="connectionstring-property-sqlserveralias-class"></a>ConnectionString 屬性 (SqlServerAlias 類別)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]取得用來建立伺服器連接別名的連接的連接字串。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.ConnectionString [= value]  
```  
  
## <a name="parts"></a>組件  
 *物件*  
 A [SqlServerAlias 類別](../../../relational-databases/wmi-provider-configuration-classes/sqlserveralias-class/sqlserveralias-class.md)物件，代表[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]別名。  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 一個字串，可指定用來為伺服器連接別名建立連接的連接字串。  
  
## <a name="remarks"></a>備註  
  
