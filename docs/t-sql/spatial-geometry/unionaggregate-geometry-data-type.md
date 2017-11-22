---
title: "UnionAggregate (geometry 資料類型) |Microsoft 文件"
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords: UnionAggregate method (geometry)
ms.assetid: dc7929cc-55ca-4a2c-a4b9-f5452f95bde8
caps.latest.revision: "13"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8883efb9f63f65034386934cf8b9b8b81d7ee6c3
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="unionaggregate-geometry-data-type"></a>UnionAggregate (geometry 資料類型)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

在一組 geometry 物件上執行聯集作業。
  
## <a name="syntax"></a>語法  
  
```  
  
UnionAggregate ( geometry_operand )  
```  
  
## <a name="arguments"></a>引數  
 *geometry_operand*  
 是**幾何**類型資料表資料行包含一組**幾何**物件在其上執行聯集作業。  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回型別：**幾何**  
  
## <a name="exceptions"></a>例外狀況  
 輸入的值無效時，會擲回 `FormatException`。 請參閱[STIsValid &#40; geometry 資料類型 &#41;](../../t-sql/spatial-geometry/stisvalid-geometry-data-type.md)  
  
## <a name="remarks"></a>備註  
 方法會傳回**null**當輸入是空的或輸入具有不同的 Srid。 請參閱[空間參考識別碼 &#40;Srid &#41;](../../relational-databases/spatial/spatial-reference-identifiers-srids.md)  
  
 方法會忽略**null**輸入。  
  
> [!NOTE]  
>  方法會傳回**null**如果所有輸入的值為**null**。  
  
## <a name="examples"></a>範例  
 下列範例會傳回一組的聯集**幾何**資料表變數中的物件。  
 ```
 -- Setup table variable for UnionAggregate example 
 DECLARE @Geom TABLE 
 ( 
 shape geometry, 
 shapeType nvarchar(50) 
 ); 
 INSERT INTO @Geom(shape,shapeType) 
 VALUES('CURVEPOLYGON(CIRCULARSTRING(2 3, 4 1, 6 3, 4 5, 2 3))', 'Circle'), 
 ('POLYGON((1 1, 4 1, 4 5, 1 5, 1 1))', 'Rectangle'); 
 -- Perform UnionAggregate on @Geom.shape column 
 SELECT geometry::UnionAggregate(shape).ToString() 
 FROM @Geom;
``` 
  
## <a name="see-also"></a>請參閱＜  
 [擴充的靜態幾何方法](../../t-sql/spatial-geometry/extended-static-geometry-methods.md)  
  
  

