---
title: STContains (geometry 資料型別) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STContains (geometry Data Type)
- STContains_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STContains (geometry Data Type)
ms.assetid: 865ceca1-9200-45ed-a7d8-e286e2679fdc
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 1a8d85b5823d692343acbc73ffc10e0cb08bc9f9
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "67930150"
---
# <a name="stcontains-geometry-data-type"></a>STContains (geometry 資料類型)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

如果 **geometry** 執行個體完整包含另一個 **geometry** 執行個體，則會傳回 1。 如果不是則傳回 0。
  
## <a name="syntax"></a>語法  
  
```  
  
.STContains ( other_geometry )  
```  
  
## <a name="arguments"></a>引數  
 *other_geometry*  
 這是要與叫用 **所在之執行個體相比較的另一個**geometry`STContains()` 執行個體。  
  
## <a name="return-types"></a>傳回型別  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**bit**  
  
 CLR 傳回類型：**SqlBoolean**  
  
## <a name="remarks"></a>備註  
 如果 `STContains()`geometry **執行個體的空間參考識別碼 (SRID) 不相符，** 一定會傳回 Null。  
  
## <a name="examples"></a>範例  
 下列範例會使用 `STContains()` 來測試兩個 `geometry` 執行個體，看看第一個執行個體是否包含第二個執行個體。  
  
```  
DECLARE @g geometry;  
DECLARE @h geometry;  
SET @g = geometry::STGeomFromText('POLYGON((0 0, 2 0, 2 2, 0 2, 0 0))', 0);  
SET @h = geometry::STGeomFromText('POINT(1 1)', 0);  
SELECT @g.STContains(@h);  
```  
  
## <a name="see-also"></a>另請參閱  
 [空間索引概觀](../../relational-databases/spatial/spatial-indexes-overview.md)   
 [幾何例項上的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

