---
title: "STIsValid (geometry 資料類型) |Microsoft 文件"
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
- STIsValid (geometry Data Type)
- STIsValid_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STIsValid (geometry Data Type)
ms.assetid: 6da39bea-0f67-4660-98fc-d7214f9b2138
caps.latest.revision: 23
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3726790e2d4b5cfc235ca59f96e4247726161bf7
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="stisvalid-geometry-data-type"></a>STIsValid (geometry 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

傳回 true，否則**幾何**執行個體而言是否格式正確，根據它的開放式地理空間協會 (OGC) 類型。 傳回 false 如果**幾何**執行個體不是語式正確。
  
## <a name="syntax"></a>語法  
  
```  
  
.STIsValid ( )  
```  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回型別：**位元**  
  
 CLR 傳回類型： **SqlBoolean**  
  
## <a name="remarks"></a>備註  
 OGC 類型**幾何**執行個體由叫用[stgeometrytype （)](../../t-sql/spatial-geometry/stgeometrytype-geometry-data-type.md)。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]只會產生有效**幾何**例項，但是允許儲存和擷取無效的執行個體。 可以使用 `MakeValid()` 方法來擷取表示任何無效例項之相同點組的有效例項。  
  
## <a name="examples"></a>範例  
 下列範例會建立 `geometry` 例項，並使用 `STIsValid()` 來測試此例項是否有效。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 1 0)', 0);  
SELECT @g.STIsValid();  
```  
  
## <a name="see-also"></a>另請參閱  
 [STGeometryType &#40; geometry 資料類型 &#41;](../../t-sql/spatial-geometry/stgeometrytype-geometry-data-type.md)   
 [MakeValid &#40;geometry 資料類型&#41;](../../t-sql/spatial-geometry/makevalid-geometry-data-type.md)   
 [幾何例項上的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  


