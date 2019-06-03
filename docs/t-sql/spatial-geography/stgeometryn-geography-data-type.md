---
title: STGeometryN (geography 資料型別) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STGeometryN (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STGeometryN method
ms.assetid: 53755f69-cd50-475b-b3b8-a1a9157cf03a
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: 0955e653c2181cb8004780a8695c06c5c99a593f
ms.sourcegitcommit: 57c3b07cba5855fc7b4195a0586b42f8b45c08c2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/20/2019
ms.locfileid: "65936874"
---
# <a name="stgeometryn-geography-data-type"></a>STGeometryN (geography 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  傳回 **GeometryCollection** 中指定的 **geography** 元素或是它的其中一個子類型。 當在 **GeometryCollection** 的子類型 (例如 **MultiPoint** 或 **MultiLineString**) 上使用 STGeometryN() 時，如果使用 N = 1 呼叫，這個方法會傳回 **geography** 執行個體。  
  
## <a name="syntax"></a>語法  
  
```  
  
.STGeometryN ( expression )  
```  
  
## <a name="arguments"></a>引數  
 *expression*  
 這是介於 1 和 **GeometryCollection** 內的 **geography** 執行個體數目之間的 **int** 運算式。  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**geography**  
  
 CLR 傳回型別：**SqlGeography**  
  
## <a name="remarks"></a>Remarks  
 如果參數大於 [STNumGeometries()](../../t-sql/spatial-geography/stnumgeometries-geography-data-type.md) 的結果，這個方法會傳回 null；如果 *expression* 參數小於 1，將會擲回 **ArgumentOutOfRangeException**。  
  
## <a name="examples"></a>範例  
 下列範例會建立 `MultiPoint``geography` 執行個體，並使用 `STGeometryN()` 來尋找 **GeometryCollection** 的第二個 `geography` 執行個體。  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('MULTIPOINT(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STGeometryN(2).ToString();  
```  
  
## <a name="see-also"></a>另請參閱  
 [地理例項上的 OGC 方法](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
