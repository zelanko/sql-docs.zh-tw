---
title: "STDifference (geography 資料類型) |Microsoft 文件"
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
f1_keywords:
- STDifference_TSQL
- STDifference (geography Data Type)
dev_langs: TSQL
helpviewer_keywords: STDifference (geography Data Type)
ms.assetid: 1cde5054-b91a-41bb-812a-08c9308738af
caps.latest.revision: "20"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9898254d43c4586f787d5e7eb68e457137be5554
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="stdifference-geography-data-type"></a>STDifference (geography 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  傳回物件，表示的點集合從一**geography**體外之某個執行個體**geography**執行個體。  
  
## <a name="syntax"></a>語法  
  
```  
  
.STDifference ( other_geography )  
```  
  
## <a name="arguments"></a>引數  
 *other_geography*  
 這是另一個**geography**執行個體表示的正在叫用 stdifference （） 執行個體移除哪些點。  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回型別：**地理位置**  
  
 CLR 傳回類型： **SqlGeography**  
  
## <a name="exceptions"></a>例外狀況  
 這個方法會擲回**ArgumentException**如果執行個體包含對蹠邊緣。  
  
## <a name="remarks"></a>備註  
 如果這個方法永遠傳回 null 的空間參考識別碼 (Srid) **geography**例項不相符。  
  
 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，傳回伺服器上的可能結果集已擴充到**FullGlobe**執行個體。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援大於半球的空間執行個體。 只有當輸入執行個體包含圓弧線段時，結果才能包含圓弧線段。 這個方法並不精確。  
  
## <a name="examples"></a>範例  
  
### <a name="a-computing-the-difference-between-two-geography-instances"></a>A. 計算兩個地理位置執行個體之間的差異  
 下列範例會使用`STDifference()`來計算兩個之間的差異**geography**執行個體。  
  
```  
DECLARE @g geography;  
DECLARE @h geography;  
SET @g = geography::STGeomFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))', 4326);  
SET @h = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STDifference(@h).ToString();  
```  
  
### <a name="b-using-a-fullglobe-with-stdifference"></a>B. 使用 FullGlobe 來搭配 STDifference()  
 下列範例使用 `FullGlobe` 執行個體。 第一個結果是空白 `GeometryCollection`，第二個結果是 `Polygon` 執行個體。 當 `STDifference()` 執行個體為參數時，`GeometryCollection` 會傳回空白 `FullGlobe`。 `geography` 叫用執行個體中的每個點都包含在 `FullGlobe` 執行個體。  
  
```
 DECLARE @g geography = 'POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))';  
 DECLARE @h geography = 'FULLGLOBE';  
 SELECT @g.STDifference(@h).ToString(),  
 @h.STDifference(@g).ToString();
 ```  
  
## <a name="see-also"></a>另請參閱  
 [地理例項上的 OGC 方法](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
