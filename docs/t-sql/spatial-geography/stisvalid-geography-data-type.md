---
title: "STIsValid (geography 資料類型) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- STIsValid method (geography)
ms.assetid: 1bfe787f-ddf0-4fc7-af6a-570a58faab23
caps.latest.revision: 11
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2149008613cf38f1d4e3ac138afd776e16f4250b
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="stisvalid-geography-data-type"></a>STIsValid (geography 資料類型)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  傳回 true，否則**geography**執行個體是格式正確而且辨識為有效的地理位置物件根據它的開放式地理空間協會 (OGC) 類型。 傳回 false 如果**geography**執行個體不是語式正確。 這個方法是精確的。  
  
 這個 geography 資料類型方法可支援**FullGlobe**執行個體或大於半球的空間執行個體。  
  
## <a name="syntax"></a>語法  
  
```  
  
.STIsValid ( )  
```  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回型別：**位元**  
  
 CLR 傳回類型： **SqlBoolean**  
  
## <a name="remarks"></a>備註  
 OGC 類型**geography**執行個體由叫用[stgeometrytype （)](../../t-sql/spatial-geography/stgeometrytype-geography-data-type.md)。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]只會產生有效**geography**例項，但是允許儲存和擷取無效的執行個體。 可以使用 `MakeValid()` 方法來擷取表示無效執行個體之相同點組的有效執行個體。  
  
## <a name="examples"></a>範例  
 下列範例會建立 `geography` 例項，並使用 `STIsValid()` 來測試此例項是否有效。  
  
```  
DECLARE @g geography = geography::STGeomFromText('LINESTRING(0 0, 2 2, 1 0)', 4326);  
SELECT @g.STIsValid();  
DECLARE @g geography  
```  
  
## <a name="see-also"></a>另請參閱  
 [STGeometryType &#40; geography 資料類型 &#41;](../../t-sql/spatial-geography/stgeometrytype-geography-data-type.md)   
 [MakeValid &#40;geography 資料類型&#41;](../../t-sql/spatial-geography/makevalid-geography-data-type.md)   
 [Geography 執行個體上的 OGC 方法](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
