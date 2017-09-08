---
title: "STGeometryN (geography 資料類型) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STGeometryN (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STGeometryN method
ms.assetid: 53755f69-cd50-475b-b3b8-a1a9157cf03a
caps.latest.revision: 15
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d5d11dc77ce692543068cba6739ef982bc8264c8
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="stgeometryn-geography-data-type"></a>STGeometryN (geography 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

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
  
## <a name="see-also"></a>另請參閱  
 [Geography 執行個體上的 OGC 方法](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
