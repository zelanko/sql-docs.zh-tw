---
title: "STGeometryN (geometry 資料類型) |Microsoft 文件"
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STGeometryN_TSQL
- STGeometryN (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STGeometryN (geometry Data Type)
ms.assetid: 348c7047-3442-4590-8879-fe841e79058c
caps.latest.revision: 19
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: fe227cc574662025aa43016ca3f053ad36bf0678
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="stgeometryn-geometry-data-type"></a>STGeometryN (geometry 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

傳回在指定的幾何**幾何集合**。
  
## <a name="syntax"></a>語法  
  
```  
  
.STGeometryN ( expression )  
```  
  
## <a name="arguments"></a>引數  
 *expression*  
 是**int** 1 之間的數字的運算式**幾何**中執行個體**geometrycollection**。  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回型別：**幾何**  
  
 CLR 傳回類型： **SqlGeometry**  
  
## <a name="remarks"></a>備註  
 這個方法會傳回**null**如果參數大於的結果`STNumGeometries()`將會擲回**ArgumentOutOfRangeException**如果*運算式*參數是小於 1。  
  
## <a name="examples"></a>範例  
 下列範例會建立`MultiPoint``geometry collection`並用`STGeometryN()`尋找第二個`geometry`集合執行個體。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('MULTIPOINT(0 0, 13.5 2, 7 19)', 0);  
SELECT @g.STGeometryN(2).ToString();  
```  
  
## <a name="see-also"></a>另請參閱  
 [幾何例項上的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  


