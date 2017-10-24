---
title: "STConvexHull (geometry 資料類型) |Microsoft 文件"
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
- STConvexHull (geometry Data Type)
- STConvexHull_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STConvexHull (geometry Data Type)
ms.assetid: 60a520a6-1a7c-486b-8d91-34401edf6233
caps.latest.revision: 22
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7bfd196565b33604a02a68b1380f676e7e730c45
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="stconvexhull-geometry-data-type"></a>STConvexHull (geometry 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

傳回代表項之凸面的物件**幾何**執行個體。
  
## <a name="syntax"></a>語法  
  
```  
  
.STConvexHull ( )  
```  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回型別：**幾何**  
  
 CLR 傳回類型： **SqlGeometry**  
  
## <a name="remarks"></a>備註  
 `STConvexHull()`傳回包含最小凸面多邊形給定**幾何**執行個體。 **點**或共線**LineString**執行個體將會產生與輸入相同類型的執行個體。  
  
## <a name="examples"></a>範例  
 下列範例會使用 `STConvexHull()` 來尋找非凸面 `Polygon``geometry` 執行個體的凸面。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POLYGON((0 0, 0 2, 1 1, 2 2, 2 0, 0 0))', 0);  
SELECT @g.STConvexHull().ToString();  
```  
  
## <a name="see-also"></a>另請參閱  
 [幾何例項上的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  


