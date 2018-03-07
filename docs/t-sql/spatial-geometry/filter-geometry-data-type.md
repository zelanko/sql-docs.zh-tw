---
title: "篩選器 (geometry 資料類型) |Microsoft 文件"
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- Filter
- Filter_TSQL
- Filter (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- Filter method
ms.assetid: 3d629a39-157e-4159-a3ca-a3c2e0ed4160
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e09f4ac5d6d4ecaf32f6b500aee9a3a50c772c02
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="filter-geometry-data-type"></a>Filter (geometry 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

這個方法提供快速且僅限索引的交集方法，來判斷**幾何**執行個體相交，另一個**幾何**執行個體，假設有索引可用。
  
傳回 1，如果**幾何**可能執行個體相交另**幾何**執行個體。 這個方法可能會產生誤判傳回值，且確切的結果可能會依計畫而定。 如果沒有的交集會傳回精確的 0 值 （真否定傳回）**幾何**找到執行個體。
  
在其中索引無法使用，或未使用的情況下，則方法會傳回相同的值**stintersects （)**時使用相同的參數來呼叫。
  
## <a name="syntax"></a>語法  
  
```  
  
.Filter ( other_geometry )  
```  
  
## <a name="arguments"></a>引數  
 *other_geometry*  
 這是另一個**幾何**比較 Filter() 叫用所在的執行個體的執行個體。  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回型別：**位元**  
  
 CLR 傳回類型： **SqlBoolean**  
  
## <a name="remarks"></a>備註  
 這個方法不具決定性或並非精確的。  
  
## <a name="examples"></a>範例  
 下列範例使用 `Filter()` 來判斷兩個 `geometry` 執行個體是否相交。  
  
```  
CREATE TABLE sample (id int primary key, g geometry);  
GO  
INSERT INTO sample VALUES  
   (0, geometry::Point(0, 0, 0)),  
   (1, geometry::Point(0, 1, 0)),  
   (2, geometry::Point(0, 2, 0)),  
   (3, geometry::Point(0, 3, 0)),  
   (4, geometry::Point(0, 4, 0));  
  
CREATE SPATIAL INDEX sample_idx ON sample(g)  
WITH (bounding_box = (-8000, -8000, 8000, 8000));  
GO  
SELECT id  
FROM sample   
WHERE g.Filter(geometry::Parse('POLYGON((-1 -1, 1 -1, 1 1, -1 1, -1 -1))')) = 1;  
```  
  
## <a name="see-also"></a>另請參閱  
 [幾何例項上擴充的方法](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)   
 [STIntersects &#40;geometry 資料類型&#41;](../../t-sql/spatial-geometry/stintersects-geometry-data-type.md)  
  
  

