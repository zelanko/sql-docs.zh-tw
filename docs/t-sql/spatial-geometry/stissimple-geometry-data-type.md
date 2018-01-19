---
title: "STIsSimple (geometry 資料類型) |Microsoft 文件"
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
- STIsSimple_TSQL
- STIsSimple (geometry Data Type)
dev_langs: TSQL
helpviewer_keywords: STIsSimple (geometry Data Type)
ms.assetid: da8f45d4-4f9c-405d-b883-760eb5344a71
caps.latest.revision: "20"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 52c407fb89544ef7857ffd5ac3dae00a9c4e233c
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/19/2018
---
# <a name="stissimple-geometry-data-type"></a>STIsSimple (geometry 資料類型)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

傳回 1，如果**幾何**例項是簡單，由開放式地理空間協會 (OGC) 所定義。 傳回 0，如果**幾何**執行個體不是簡單。
  
## <a name="syntax"></a>語法  
  
```  
  
.STIsSimple ( )  
```  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回型別：**位元**  
  
 CLR 傳回類型： **SqlBoolean**  
  
## <a name="remarks"></a>備註  
 若要是簡單、**幾何**執行個體必須符合下列需求：  
  
-   此例項的每一個圖形都不能自己相交 (除了在它的端點上以外)。  
  
-   此例項的兩個圖形不能在非兩者界限內的點上彼此相交。  
  
## <a name="examples"></a>範例  
 下列範例會建立與自己相交的非簡單式 `LineString` 例項，並使用 `STIsSimple()` 來測試看看 `LineString` 是否為簡單的例項。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 0 2, 2 0)', 0);  
SELECT @g.STIsSimple();  
```  
  
## <a name="see-also"></a>另請參閱  
 [幾何例項上的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

