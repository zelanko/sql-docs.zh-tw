---
title: Filter (geometry 資料類型) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e36a0baf3228e8ff398fb9d2236b17d38c54d15d
ms.sourcegitcommit: a6596c62f607041c4402f7d5b41a232fca257c14
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36254000"
---
# <a name="filter-geometry-data-type"></a>Filter (geometry 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

這個方法提供快速且僅限索引的交集方法，可判斷 **geometry** 執行個體是否與另一個 **geometry** 執行個體相交 (假設有提供索引)。
  
如果 **geometry** 執行個體可能與另一個 **geometry** 執行個體相交，則會傳回 1。 這個方法可能會產生誤判傳回值，且確切的結果可能會依計畫而定。 如果未找到任何 **geometry** 執行個體相交，則傳回正確的 0 值 (真否定傳回值)。
  
在沒有提供索引或未使用索引的情況下，以相同的參數呼叫時，此方法所傳回的值會與 **STIntersects()** 相同。
  
## <a name="syntax"></a>語法  
  
```  
  
.Filter ( other_geometry )  
```  
  
## <a name="arguments"></a>引數  
 *other_geometry*  
 這是要與叫用 Filter() 所在之執行個體相比較的另一個 **geometry** 執行個體。  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**bit**  
  
 CLR 傳回類型：**SqlBoolean**  
  
## <a name="remarks"></a>Remarks  
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
 [幾何執行個體上擴充的方法](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)   
 [STIntersects &#40;geometry 資料類型&#41;](../../t-sql/spatial-geometry/stintersects-geometry-data-type.md)  
  
  

