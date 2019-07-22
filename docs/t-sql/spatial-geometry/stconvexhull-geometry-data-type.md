---
title: STConvexHull (geometry 資料類型) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STConvexHull (geometry Data Type)
- STConvexHull_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STConvexHull (geometry Data Type)
ms.assetid: 60a520a6-1a7c-486b-8d91-34401edf6233
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: d9244a2833a75925fab1f00d6ce20915f5ceaafb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67930330"
---
# <a name="stconvexhull-geometry-data-type"></a>STConvexHull (geometry 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

傳回代表 **geometry** 執行個體凸殼的物件。
  
## <a name="syntax"></a>語法  
  
```  
  
.STConvexHull ( )  
```  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**geometry**  
  
 CLR 傳回型別：**SqlGeometry**  
  
## <a name="remarks"></a>Remarks  
 `STConvexHull()` 會傳回包含所指定 **geometry** 執行個體的最小凸面多邊形。 **Points** 或共線 **LineString** 執行個體將會產生與輸入相同類型的執行個體。  
  
## <a name="examples"></a>範例  
 下列範例會使用 `STConvexHull()` 來尋找非凸面 `Polygon``geometry` 執行個體的凸面。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POLYGON((0 0, 0 2, 1 1, 2 2, 2 0, 0 0))', 0);  
SELECT @g.STConvexHull().ToString();  
```  
  
## <a name="see-also"></a>另請參閱  
 [幾何例項上的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

