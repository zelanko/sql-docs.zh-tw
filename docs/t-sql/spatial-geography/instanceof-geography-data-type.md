---
title: InstanceOf (geography 資料類型) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- InstanceOf
- InstanceOf_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- InstanceOf method
ms.assetid: 1eaed0e4-1c72-45a9-9926-5b513335cf33
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: 52ec2695b24a2a900e84b6a186802024d47b7613
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65937723"
---
# <a name="instanceof-geography-data-type"></a>InstanceOf (geography 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

測試 **geography** 執行個體是否與指定的類型相同。  
  
## <a name="syntax"></a>語法  
  
```sql  
  
.InstanceOf ( 'geography_type')  
```  
  
## <a name="arguments"></a>引數  
*geography_type*  
這是 **nvarchar(4000)** 字串，它會指定在 **geography** 類型階層內公開之 16 種類型的其中一種。  
  
## <a name="return-types"></a>傳回類型  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**bit**  
  
CLR 傳回型別：**SqlBoolean**  
  
## <a name="remarks"></a>Remarks  
如果 **geography** 執行個體的類型與指定的類型相同，或是指定的類型是此執行個體類型的上階，則會傳回 1，否則會傳回 0。  
  
這個 **geography** 資料類型方法可支援 **FullGlobe** 執行個體或大於半球的空間執行個體。  
  
此方法的輸入必須為下列其中一種類型：Geometry、Point、Curve、LineString、CircularString、Surface、Polygon、CurvePolygon、**GeometryCollection**、**MultiSurface**、**MultiPolygon、MultiCurve、MultiLineString**、**MultiPoint** 或 **FullGlobe**。  
  
如果輸入有使用任何其他字串，這個方法會擲回 `ArgumentException`。  
  
這個方法並不精確。  
  
## <a name="examples"></a>範例  
下列範例會建立 `MultiPoint` 執行個體，並使用 `InstanceOf()` 來查看此執行個體是否為 `GeometryCollection`。  
  
```sql  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('MULTIPOINT(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.InstanceOf('GEOMETRYCOLLECTION');  
```  
  
## <a name="see-also"></a>另請參閱  
 [地理例項上擴充的方法](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
