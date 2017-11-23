---
title: "狀態屬性 （SqlService 類別） |Microsoft 文件"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: wmi
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname: State Property (SqlService Class)
apilocation: sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords: State property
ms.assetid: 9e09f419-947c-4d4b-9a49-2d3396c847cd
caps.latest.revision: "36"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 31b49dea8026ee0aae4406451179ee8bafd5c712
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="state-property-sqlservice-class"></a>State 屬性 (SqlService 類別)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]取得或設定服務的目前狀態。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.State [= value]  
```  
  
## <a name="parts"></a>組件  
 *物件*  
 表示此服務的 [SqlService 類別](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) 物件。  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 指定服務狀態的 uint32 值。  
  
 它可以是下列其中一個值。  
  
 1  
 已停止。 服務已停止。  
  
 2  
 開始暫止。 服務正在等候開始。  
  
 3  
 停止暫止。 服務正在等候停止。  
  
 4  
 執行中。 服務正在執行中。  
  
 5  
 繼續暫止。 服務正在等候繼續。  
  
 6  
 暫停暫止。 服務正在等候暫停。  
  
 7  
 已暫停。 服務已暫停。  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>請參閱＜  
 [啟動及停止服務](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
