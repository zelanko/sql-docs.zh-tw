---
title: "STNumGeometries (geometry 資料類型) |Microsoft 文件"
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STNumGeometries (geometry Data Type)
- STNumGeometries_TSQL
dev_langs: TSQL
helpviewer_keywords: STNumGeometries (geometry Data Type)
ms.assetid: 9402b03d-3039-42ca-ac59-f96b7f1a48de
caps.latest.revision: "22"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f1909f0d094ce1cfe170389de6ccd9c57f5503a8
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="stnumgeometries-geometry-data-type"></a>STNumGeometries (geometry 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

傳回組成的幾何數目**幾何**執行個體。
  
## <a name="syntax"></a>語法  
  
```  
  
.STNumGeometries ( )  
```  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回型別： **int**  
  
 CLR 傳回類型： **SqlInt32**  
  
## <a name="remarks"></a>備註  
 這個方法會傳回 1，如果**幾何**執行個體不是**MultiPoint**， **MultiLineString**， **MultiPolygon**，或**GeometryCollection**執行個體，便傳回 0**幾何**是空的執行個體。  
  
> [!NOTE]  
>  如果**GeometryCollection**有巢狀的空項目，`STNumGeometries()`不會傳回 0。 雖然中的項目**GeometryCollection**執行個體是空的該執行個體本身不是空的集合。  
  
  

