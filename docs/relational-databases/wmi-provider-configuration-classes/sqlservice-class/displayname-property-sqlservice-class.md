---
title: "DisplayName 屬性 （SqlService 類別） |Microsoft 文件"
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
apiname: DisplayName Property (SqlService Class)
apilocation: sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords: DisplayName property
ms.assetid: 49c408aa-6eb4-45cd-8d5c-60f065f24f5c
caps.latest.revision: "35"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 20c247d8581099dc797c2ea05fc2eab91dfcb51a
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="displayname-property-sqlservice-class"></a>DisplayName 屬性 (SqlService 類別)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]取得服務的顯示名稱。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.DisplayName [= value]  
```  
  
## <a name="parts"></a>組件  
 *物件*  
 表示此服務的 [SqlService 類別](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) 物件。  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 指定此服務之顯示名稱的字串值。  
  
## <a name="remarks"></a>備註  
 這個字串的最大長度為 256 個字元。 此名稱在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 組態管理員中有保留大小寫。 不過，顯示名稱比較一定不區分大小寫。  
  
## <a name="example"></a>範例  
  
```  
mysqlservice.DisplayName = "Atdisk"  
```  
  
## <a name="see-also"></a>請參閱＜  
 [啟動及停止服務](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
