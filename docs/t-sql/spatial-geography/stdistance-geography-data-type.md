---
title: STDistance (geography 資料型別) | Microsoft Docs
ms.custom: ''
ms.date: 11/19/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STDistance_TSQL
- STDistance (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STDistance method
ms.assetid: 063d8722-e019-4d3d-8fcf-dbf5325823e7
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 795fa917f598ed1dd477916f42808d4abb0c8a69
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/21/2020
ms.locfileid: "86555153"
---
# <a name="stdistance-geography-data-type"></a>STDistance (geography 資料類型)
[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

  傳回a **geography** 執行個體中的點與另一個 **geography** 執行個體中的點之間的最短距離。  
  
> [!NOTE]  
>  `STDistance()` 會傳回兩個 geography 型別之間的最短 **LineString**。 這是地理距離的近似值。 通用地球模型上 `STDistance()` 與實際地理距離的偏差不大於 .25%。 這可避免地理類型中長度與距離細微差異的混淆。  
  
## <a name="syntax"></a>語法  
  
```  
  
.STDistance ( other_geography )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引數
 *other_geography*  
 這是另一個 **geography** 執行個體，用來測量它與 STDistance() 叫用所在之執行個體之間的距離。 如果 *other_geography* 為空白集合，STDistance() 會傳回 null。  
  
## <a name="return-types"></a>傳回型別  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**float**  
  
 CLR 傳回類型：**SqlDouble**  
  
## <a name="remarks"></a>備註  
 表達結果的測量單位是由空間資料的[空間參考識別碼 &#40;SRID&#41;](../../relational-databases/spatial/spatial-reference-identifiers-srids.md) 定義。
如果 **geography** 執行個體的空間參考識別碼 (SRID) 不相符，STDistance() 一定會傳回 *null*。  
  
> [!NOTE]  
>  **geography** 資料型別上計算區域或距離的方法將會根據此方法中使用之執行個體的 SRID，而傳回不同的結果。 如需有關 SRID 的詳細資訊，請參閱[空間參考識別碼 &#40;SRIDs&#41;](../../relational-databases/spatial/spatial-reference-identifiers-srids.md)。  
  
## <a name="examples"></a>範例  
 下列範例會求得兩個 **geography** 執行個體之間的距離。  
  
```  
DECLARE @g geography;  
DECLARE @h geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SET @h = geography::STGeomFromText('POINT(-122.34900 47.65100)', 4326);  
SELECT @g.STDistance(@h);  
```  
  
## <a name="see-also"></a>另請參閱  
 [地理例項上的 OGC 方法](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
