---
title: "STIsRing (geometry 資料類型) |Microsoft 文件"
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STIsRing_TSQL
- STIsRing (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STIsRing (geometry Data Type)
ms.assetid: ea0063be-1c74-4cc4-ac6f-b65321ddfa54
caps.latest.revision: 21
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3417f5da487ea7de5d7c51820316dae3caf8bb0e
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="stisring-geometry-data-type"></a>STIsRing (geometry 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

傳回 1，如果**幾何**例項滿足以下需求：
-   它是**LineString**執行個體。  
-   它為封閉式。  
-   它為簡單式。  
-   傳回 0，如果**LineString**例項不符合需求。  

 如**幾何**執行個體為封閉式和簡單，同時[stisclosed （)](../../t-sql/spatial-geometry/stisclosed-geometry-data-type.md)和[Stissimple](../../t-sql/spatial-geometry/stissimple-geometry-data-type.md)必須傳回 1 的執行個體上叫用時。 若要判斷執行個體型別**幾何**，使用[stgeometrytype （)](../../t-sql/spatial-geometry/stgeometrytype-geometry-data-type.md)。  
  
## <a name="syntax"></a>語法  
  
```  
  
.STIsRing ( )  
```  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回型別：**位元**  
  
 CLR 傳回類型： **SqlBoolean**  
  
## <a name="remarks"></a>備註  
 如果執行個體不是 null，則這個方法會傳回**LineString**。  
  
## <a name="examples"></a>範例  
 下列範例會建立 `LineString` 例項，並使用 `STIsRing()` 來測試看看此例項是不是環形。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 1 0, 0 0)', 0);  
SELECT @g.STIsRing();  
```  
  
## <a name="see-also"></a>另請參閱  
 [STIsClosed &#40;geometry 資料類型&#41;](../../t-sql/spatial-geometry/stisclosed-geometry-data-type.md)   
 [STGeometryType &#40; geometry 資料類型 &#41;](../../t-sql/spatial-geometry/stgeometrytype-geometry-data-type.md)   
 [STIsSimple &#40; geometry 資料類型 &#41;](../../t-sql/spatial-geometry/stissimple-geometry-data-type.md)   
 [幾何例項上的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  


