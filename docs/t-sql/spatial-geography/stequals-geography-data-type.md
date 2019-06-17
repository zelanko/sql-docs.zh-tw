---
title: STEquals (geography 資料類型) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STEquals_TSQL
- STEquals (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STEquals method
ms.assetid: 0766ff37-0b9e-49bf-83c0-019f4354fe44
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: e12465bf75cb6619e837ba55eaca09231cc4b5e8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65936963"
---
# <a name="stequals-geography-data-type"></a>STEquals (geography 資料類型)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  如果 **geography** 執行個體表示設定為與另一個 **geography** 執行個體相同的點，就會傳回 1。 如果不是則傳回 0。  
  
## <a name="syntax"></a>語法  
  
```  
  
.STEquals ( other_geography )  
```  
  
## <a name="arguments"></a>引數  
 *other_geography*  
 這是要與叫用 `STEquals()` 所在之執行個體相比較的另一個 **geography** 執行個體。  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**bit**  
  
 CLR 傳回型別：**SqlBoolean**  
  
## <a name="remarks"></a>Remarks  
 如果 **geography** 執行個體的空間參考識別碼 (SRID) 不相符，這個方法一律會傳回 null。  
  
## <a name="examples"></a>範例  
 下列範例會建立兩個 `geography` 執行個體 (兩者的 `STGeomFromText()` 相同，但兩者並不完全相同)，並使用 `STEquals()` 來測試其是否相等。 這些例項相等，因為 `LINESTRING` 和 `POINT` 包含在 `POLYGON` 內。  
  
```  
DECLARE @g geography;  
DECLARE @h geography;  
SET @g = geography::STGeomFromText('GEOMETRYCOLLECTION(POLYGON((-122.368 47.658, -122.338 47.649, -122.338 47.658, -122.368 47.658, -122.368 47.658)), LINESTRING(-122.360 47.656, -122.343 47.656), POINT (-122.35 47.656))', 4326);  
SET @h = geography::STGeomFromText('POLYGON((-122.368 47.658, -122.338 47.649, -122.338 47.658, -122.368 47.658, -122.368 47.658))', 4326);  
SELECT @g.STEquals(@h);  
```  
  
## <a name="see-also"></a>另請參閱  
 [地理例項上的 OGC 方法](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
