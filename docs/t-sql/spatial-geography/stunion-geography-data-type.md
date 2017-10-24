---
title: "STUnion (geography 資料類型) |Microsoft 文件"
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
- STUnion (geography Data Type)
- STUnion_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STUnion method
ms.assetid: 9bf87691-efd8-4c53-bd2f-eefe0acd19ca
caps.latest.revision: 23
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5e200f81a17e9b512986795077fe487e54a489f2
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="stunion-geography-data-type"></a>STUnion (geography 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  傳回物件，表示的聯集**geography**與另一個執行個體**geography**執行個體。  
  
## <a name="syntax"></a>語法  
  
```  
  
.STUnion ( other_geography )  
```  
  
## <a name="arguments"></a>引數  
 *other_geography*  
 這是另一個**geography**形成聯 stunion （） 在其叫用的執行個體的執行個體。  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回型別：**地理位置**  
  
 CLR 傳回類型： **SqlGeography**  
  
## <a name="exceptions"></a>例外狀況  
 這個方法會擲回**ArgumentException**如果執行個體包含對蹠邊緣。  
  
## <a name="remarks"></a>備註  
 如果這個方法永遠傳回 null 的空間參考識別碼 (Srid) **geography**例項不相符。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援大於半球的空間執行個體。 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，傳回伺服器上的可能結果集已擴充到**FullGlobe**執行個體。  
  
 只有當輸入執行個體包含圓弧線段時，結果才能包含圓弧線段。  
  
 這個方法並不精確。  
  
## <a name="examples"></a>範例  
  
### <a name="a-computing-the-union-of-two-polygons"></a>A. 計算兩個多邊形的聯集  
 下列範例使用 `STUnion()` 來計算兩個 `Polygon` 執行個體的聯集。  
  
```  
DECLARE @g geography;  
DECLARE @h geography;  
SET @g = geography::STGeomFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))', 4326);  
SET @h = geography::STGeomFromText('POLYGON((-122.351 47.656, -122.341 47.656, -122.341 47.661, -122.351 47.661, -122.351 47.656))', 4326);  
SELECT @g.STUnion(@h).ToString();  
```  
  
### <a name="b-producing-a-fullglobe-result"></a>B. 產生 FullGlobe 結果  
 下列範例會在 `FullGlobe` 結合了兩個 `STUnion()` 執行個體時產生 `Polygon`。  
  
```
 DECLARE @g geography = 'POLYGON ((-122.358 47.653, -122.358 47.658,-122.348 47.658, -122.348 47.649, -122.358 47.653))';  
 DECLARE @h geography = 'POLYGON ((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))';  
 SELECT @g.STUnion(@h).ToString();
 ```  
  
### <a name="c-producing-a-triagonal-hole-from-a-union-of-a-curvepolygon-and-a-traigonal-hole"></a>C. 從 CurvePolygon 和三角洞的聯集產生三角洞  
 下列範例會從 `CurvePolygon` 與 `Polygon` 執行個體的聯集產生三角洞。  
  
```
 DECLARE @g geography = 'POLYGON ((-0.5 0, 0 1, 0.5 0.5, -0.5 0))';  
 DECLARE @h geography = 'CURVEPOLYGON(COMPOUNDCURVE(CIRCULARSTRING(0 0, 0.7 0.7, 0 1), (0 1, 0 0)))';  
 SELECT @g.STUnion(@h).ToString();
 ```  
  
## <a name="see-also"></a>另請參閱  
 [Geography 執行個體上的 OGC 方法](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  

