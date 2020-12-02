---
description: STDisjoint (geography 資料類型)
title: STDisjoint (geography 資料類型) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STDisjoint (geography Data Type)
- STDisjoint_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STDisjoint
ms.assetid: 98328a02-e018-47d6-aa93-de162b8aef62
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 14dcdd0581f88897f10160d2be70eb01bbd2b018
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "88467457"
---
# <a name="stdisjoint-geography-data-type"></a>STDisjoint (geography 資料類型)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  如果 **geography** 執行個體在空間上與另一個 **geography** 執行個體分離，則會傳回 1。 如果不是則傳回 0。  
  
## <a name="syntax"></a>語法  
  
```  
  
.STDisjoint ( other_geography )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引數
 *other_geography*  
 這是要與叫用 STDisjoint() 所在之執行個體相比較的另一個 **geography** 執行個體。  
  
## <a name="return-types"></a>傳回型別  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**bit**  
  
 CLR 傳回類型：**SqlBoolean**  
  
## <a name="remarks"></a>備註  
 如果兩個 **geography** 執行個體的點組交集是空的，表示這兩個執行個體分離。  
  
 如果 **geography** 執行個體的空間參考識別碼 (SRID) 不相符，這個方法一律會傳回 null。  
  
## <a name="examples"></a>範例  
 下列範例使用 `STDisjoint()` 來測試兩個 `geography` 例項在空間上是否分離。  
  
```  
DECLARE @g geography;  
DECLARE @h geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SET @h = geography::STGeomFromText('POINT(-122.34900 47.65100)', 4326);  
SELECT @g.STDisjoint(@h);  
```  
  
## <a name="see-also"></a>另請參閱  
 [地理位置例項上的 OGC 方法](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
