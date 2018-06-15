---
title: STUnion (geography 資料型別) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|spatial-geography
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a13ebe94c849f8ae9a2a89c38a101d67b9a3f653
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "33064725"
---
# <a name="stunion-geography-data-type"></a>STUnion (geography 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  傳回物件，表示 **geography** 執行個體與另一個 **geography** 執行個體的聯集。  
  
## <a name="syntax"></a>語法  
  
```  
  
.STUnion ( other_geography )  
```  
  
## <a name="arguments"></a>引數  
 *other_geography*  
 這是另一個要與 STUnion() 叫用所在的執行個體形成聯集的 **geography** 執行個體。  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**geography**  
  
 CLR 傳回類型：**SqlGeography**  
  
## <a name="exceptions"></a>例外狀況  
 如果執行個體包含對蹠邊緣，這個方法會擲回 **ArgumentException**。  
  
## <a name="remarks"></a>Remarks  
 如果 **geography** 執行個體的空間參考識別碼 (SRID) 不相符，這個方法一定會傳回 null。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援大於半球的空間執行個體。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，伺服器上傳回的可能結果集已擴充到 **FullGlobe** 執行個體。  
  
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
 [地理例項上的 OGC 方法](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
