---
title: "STGeometryN (geography 資料類型) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: STGeometryN (geography Data Type)
dev_langs: TSQL
helpviewer_keywords: STGeometryN method
ms.assetid: 53755f69-cd50-475b-b3b8-a1a9157cf03a
caps.latest.revision: "15"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f0f9249552ae3c69a3dd51a7070d0f17df79c483
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="stgeometryn-geography-data-type"></a>STGeometryN (geography 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  傳回指定**geography**中的項目**GeometryCollection**或其中一個及其子型別。 子類型上使用 STGeometryN() 時**GeometryCollection**，例如**MultiPoint**或**MultiLineString**，這個方法會傳回**地理位置**如果使用 N = 1 呼叫執行個體。  
  
## <a name="syntax"></a>語法  
  
```  
  
.STGeometryN ( expression )  
```  
  
## <a name="arguments"></a>引數  
 *expression*  
 是**int** 1 之間的數字的運算式**geography**中執行個體**GeometryCollection**。  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回型別：**地理位置**  
  
 CLR 傳回類型： **SqlGeography**  
  
## <a name="remarks"></a>備註  
 這個方法會傳回 null，如果參數大於的結果[stnumgeometries （)](../../t-sql/spatial-geography/stnumgeometries-geography-data-type.md)將會擲回**ArgumentOutOfRangeException**如果*運算式*參數是小於 1。  
  
## <a name="examples"></a>範例  
 下列範例會建立`MultiPoint``geography`執行個體，並使用`STGeometryN()`尋找第二個`geography`的執行個體**GeometryCollection**。  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('MULTIPOINT(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STGeometryN(2).ToString();  
```  
  
## <a name="see-also"></a>請參閱＜  
 [地理例項上的 OGC 方法](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
