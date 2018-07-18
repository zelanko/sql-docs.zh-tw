---
title: STDifference (geometry 資料型別) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- STDifference_TSQL
- STDifference (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STDifference (geography Data Type)
ms.assetid: 1cde5054-b91a-41bb-812a-08c9308738af
caps.latest.revision: 20
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 8eeb7743ed17f9bd2bbd837b02357723cbb0f49e
ms.sourcegitcommit: a6596c62f607041c4402f7d5b41a232fca257c14
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36253930"
---
# <a name="stdifference-geography-data-type"></a>STDifference (geography 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  傳回物件，表示在另一個 **geography** 執行個體外之某個 **geography** 執行個體的點集合。  
  
## <a name="syntax"></a>語法  
  
```  
  
.STDifference ( other_geography )  
```  
  
## <a name="arguments"></a>引數  
 *other_geography*  
 這是另一個 **geography** 執行個體，指示要從 STDifference() 叫用所在的執行個體中移除哪些點。  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**geography**  
  
 CLR 傳回類型：**SqlGeography**  
  
## <a name="exceptions"></a>例外狀況  
 如果執行個體包含對蹠邊緣，這個方法會擲回 **ArgumentException**。  
  
## <a name="remarks"></a>Remarks  
 如果 **geography** 執行個體的空間參考識別碼 (SRID) 不相符，這個方法一定會傳回 null。  
  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，伺服器上傳回的可能結果集已擴充到 **FullGlobe** 執行個體。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援大於半球的空間執行個體。 只有當輸入執行個體包含圓弧線段時，結果才能包含圓弧線段。 這個方法並不精確。  
  
## <a name="examples"></a>範例  
  
### <a name="a-computing-the-difference-between-two-geography-instances"></a>A. 計算兩個地理位置執行個體之間的差異  
 下列範例使用 `STDifference()` 來計算兩個 **geography** 執行個體之間的差異。  
  
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
  
  
