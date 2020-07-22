---
title: STArea (geography 資料類型) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STArea (geography Data Type)
- STArea_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STArea method
ms.assetid: cfc0b0e0-7fde-431a-863f-d13f3b1b1bef
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 9b3b60616c146f668f7bc089a54d531ba6de78d4
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/21/2020
ms.locfileid: "86555813"
---
# <a name="starea-geography-data-type"></a>STArea (geography 資料類型)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

傳回 **geography** 執行個體的總介面區。 STArea () 的結果，是**地理**執行個體的空間參考識別碼所使用測量平方單位。 例如，如果執行個體的 SRID 是4326，則 STArea () 會以平方公尺傳回結果。  
  
## <a name="syntax"></a>語法  
  
```  
  
.STArea ( )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>傳回型別
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**float**  
  
CLR 傳回類型：**SqlDouble**  
  
## <a name="remarks"></a>備註  
如果 **geography** 執行個體僅包含 0 維度和 1 維度的圖形 (或為空白)，則 STArea() 會傳回 0。  
  
> [!NOTE]  
>  產生度量傳回值之 **geography** 資料類型上的方法將會根據此方法中使用之執行個體的 SRID 而有不同的結果。 如需有關 SRID 的詳細資訊，請參閱[空間參考識別碼 &#40;SRIDs&#41;](../../relational-databases/spatial/spatial-reference-identifiers-srids.md)。  
  
## <a name="examples"></a>範例  
下列範例會使用 `STArea()` 建立 `Polygon geography` 執行個體，並計算此多邊形的區域。  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))', 4326);  
SELECT @g.STArea();  
```  
  
## <a name="see-also"></a>另請參閱  
[地理例項上的 OGC 方法](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
