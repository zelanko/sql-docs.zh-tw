---
description: Filter (geography 資料類型)
title: Filter (geography 資料類型) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 4a5e5ff41504184bd8c1aa0805267f38566b5162
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88479343"
---
# <a name="filter-geography-data-type"></a>Filter (geography 資料類型)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  這個方法提供快速且僅限索引的交集方法，可判斷 **geography** 執行個體是否與另一個 **geography** 執行個體相交 (假設有提供索引)。  
  
 如果 **geography** 執行個體有可能與另一個 **geography** 執行個體相交，則會傳回 1。 這個方法可能會產生誤判傳回值，且確切的結果可能會依計畫而定。 如果找不到任何 **geography** 執行個體相交，則傳回正確的 0 值 (真否定傳回值)。  
  
 在沒有提供索引或未使用索引的情況下，以相同的參數呼叫時，此方法所傳回的值會與 **STIntersects()** 相同。  
  
## <a name="syntax"></a>語法  
  
```  
  
.Filter ( other_geography )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引數
 *other_geography*  
 這是要與叫用 Filter() 所在之執行個體相比較的另一個 **geography** 執行個體。  
  
## <a name="return-types"></a>傳回型別  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**bit**  
  
 CLR 傳回類型：**SqlBoolean**  
  
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
 [地理執行個體上擴充的方法](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [STIntersects &#40;geography 資料類型&#41;](../../t-sql/spatial-geography/stintersects-geography-data-type.md)  
  
  
