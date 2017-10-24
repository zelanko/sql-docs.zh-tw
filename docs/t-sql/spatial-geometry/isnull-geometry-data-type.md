---
title: "IsNull (geometry 資料類型) |Microsoft 文件"
ms.custom: 
ms.date: 09/12/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- IsNull (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- IsNull (geometry Data Type)
ms.assetid: f95813a5-26c0-48aa-bfb8-56d2a0980788
caps.latest.revision: 13
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 15080827744c19120a8474f3142004c4af7a4064
ms.openlocfilehash: 5e213bd847f2d5836802d93ade5fa46f3dc3d1a9
ms.contentlocale: zh-tw
ms.lasthandoff: 09/13/2017

---
# <a name="isnull-geometry-data-type"></a>IsNull (geometry 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

型別**幾何**執行個體為 null。 如果此例項不是 Null，就會傳回 0。
  
## <a name="syntax"></a>語法  
  
```  
.IsNull  
```  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]類型：**位元**  
  
 CLR 型別： **SqlBoolean**  
  
## <a name="remarks"></a>備註  
 `IsNull`可以用來測試是否**幾何**執行個體為 null。 這會產生令人混淆的結果，當此例項不是 Null 時傳回 0，但是如果此例項為 Null 則傳回 Null。  
  
 這個方法主要是由 SQL Server 基礎結構所使用；不建議您使用 `IsNull` 來測試例項是否為 Null。  
  

## <a name="see-also"></a>另請參閱  
 [幾何例項上擴充的方法](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
  
  


