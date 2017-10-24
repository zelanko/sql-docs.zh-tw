---
title: "篩選器 (geography 資料類型) |Microsoft 文件"
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
- Filter
- Filter_TSQL
- Filter (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- Filter method
ms.assetid: 82a8f54a-3a47-4e20-b13a-b148029c5448
caps.latest.revision: 10
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 537e3a05ad368be5278eef9dc9c3d29d19754322
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="filter-geography-data-type"></a>Filter (geography 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  這個方法提供快速且僅限索引的交集方法，來判斷**geography**執行個體相交，另一個**geography**執行個體，假設有索引可用。  
  
 傳回 1，如果**geography**可能執行個體相交另**geography**執行個體。 這個方法可能會產生誤判傳回值，且確切的結果可能會依計畫而定。 如果沒有的交集會傳回精確的 0 值 （真否定傳回） **geography**找到執行個體。  
  
 在其中索引無法使用，或未使用的情況下，則方法會傳回相同的值**stintersects （)**時使用相同的參數來呼叫。  
  
## <a name="syntax"></a>語法  
  
```  
  
.Filter ( other_geography )  
```  
  
## <a name="arguments"></a>引數  
 *other_geography*  
 這是另一個**geography**比較 Filter() 叫用所在的執行個體的執行個體。  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回型別：**位元**  
  
 CLR 傳回類型： **SqlBoolean**  
  
## <a name="remarks"></a>備註  
 這個方法不具決定性或並非精確的。  
  
## <a name="examples"></a>範例  
 下列範例使用 `Filter()` 來判斷兩個 `geography` 執行個體是否相交。  
  
```  
CREATE TABLE sample (id int primary key, g geography);  
INSERT INTO sample VALUES  
   (0, geography::Point(45, -120, 4326)),  
   (1, geography::Point(45, -120.1, 4326)),  
   (2, geography::Point(45, -120.2, 4326)),  
   (3, geography::Point(45, -120.3, 4326)),  
   (4, geography::Point(45, -120.4, 4326));  
  
CREATE SPATIAL INDEX sample_idx on sample(g);  
SELECT id  
FROM sample   
WHERE g.Filter(geography::Parse(  
   'POLYGON((-120.1 44.9, -119.9 44.9, -119.9 45.1, -120.1 45.1, -120.1 44.9))')) = 1;  
```  
  
## <a name="see-also"></a>另請參閱  
 [Geography 執行個體上的擴充的方法](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [STIntersects &#40; geography 資料類型 &#41;](../../t-sql/spatial-geography/stintersects-geography-data-type.md)  
  
  

