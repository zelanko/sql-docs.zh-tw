---
title: "STDistance (geography 資料類型) |Microsoft 文件"
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
- STDistance_TSQL
- STDistance (geography Data Type)
dev_langs: TSQL
helpviewer_keywords: STDistance method
ms.assetid: 063d8722-e019-4d3d-8fcf-dbf5325823e7
caps.latest.revision: "22"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 9e0a059179710f258dae051ed7c901c1eaf27e15
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/19/2018
---
# <a name="stdistance-geography-data-type"></a>STDistance (geography 資料類型)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  傳回中點之間的最短距離**geography**執行個體和另一個點**geography**執行個體。  
  
> [!NOTE]  
>  `STDistance()`傳回最短**LineString**兩個地理位置類型。 這是地理距離的近似值。 差`STDistance()`從與實際地理距離的通用地球模型上已超過。 25%。 這可避免地理類型中長度與距離細微差異的混淆。  
  
## <a name="syntax"></a>語法  
  
```  
  
.STDistance ( other_geography )  
```  
  
## <a name="arguments"></a>引數  
 *other_geography*  
 這是另一個**geography**執行個體，用來測量 stdistance （） 叫用所在之執行個體之間的距離。 如果*other_geography*設為空白，stdistance （） 傳回 null。  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回型別： **float**  
  
 CLR 傳回類型： **SqlDouble**  
  
## <a name="remarks"></a>備註  
 Stdistance （） 永遠傳回 null，如果空間參考識別碼 (Srid) **geography**例項不相符。  
  
> [!NOTE]  
>  上的方法**geography**計算區域或距離的資料類型會傳回根據此方法中使用的執行個體的 SRID 不同的結果。   如需有關 Srid 的詳細資訊，請參閱[空間參考識別碼 &#40;Srid &#41;](../../relational-databases/spatial/spatial-reference-identifiers-srids.md).  
  
## <a name="examples"></a>範例  
 下列範例會尋找兩個距離**geography**執行個體。  
  
```  
DECLARE @g geography;  
DECLARE @h geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SET @h = geography::STGeomFromText('POINT(-122.34900 47.65100)', 4326);  
SELECT @g.STDistance(@h);  
```  
  
## <a name="see-also"></a>另請參閱  
 [地理例項上的 OGC 方法](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
