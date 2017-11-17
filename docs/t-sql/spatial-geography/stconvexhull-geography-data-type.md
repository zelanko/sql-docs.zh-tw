---
title: "STConvexHull (geography 資料類型) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
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
dev_langs:
- TSQL
helpviewer_keywords:
- STConvexHull method (geography)
ms.assetid: fb435db7-31bb-4243-9d8b-35379184cfb4
caps.latest.revision: 15
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a8376d12352994cd768b806f5ce47463196d4bfd
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="stconvexhull-geography-data-type"></a>STConvexHull (geography 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  傳回代表項之凸面的物件**geography**執行個體。  
  
## <a name="syntax"></a>語法  
  
```  
  
.STConvexHull ( )  
```  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回型別：**地理位置**  
  
 CLR 傳回類型： **SqlGeography**  
  
## <a name="remarks"></a>備註  
 傳回`FullGlobe`物件**geography**封套角度大於 90 度執行個體。  
  
 會傳回空白**geography**空的集合**geography**執行個體。  
  
 傳回**null**針對未初始化**geography**執行個體。  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-stconvexhull-on-an-uninitialized-geography-instance"></a>A. 在未初始化的 geography 執行個體上使用 STConvexHull()  
 下列範例會使用`STConvexHull()`上未初始化**geography**執行個體。  
  
```
 DECLARE @g geography;  
 SELECT @g.STConvexHull();
 ```  
  
### <a name="b-using-stconvexhull-on-an-empty-geography-instance"></a>B. 在空白的 geography 執行個體上使用 STConvexHull  
 下列範例會在空白 `STConvexHull()` 執行個體上使用 `Polygon`。  
  
```
 DECLARE @g geography = 'POLYGON EMPTY';  
 SELECT @g.STConvexHull().ToString();
 ```  
  
### <a name="c-finding-the-convex-hull-of-a-non-convex-polygon-instance"></a>C. 尋找非凸面 Polygon 執行個體的凸面  
 下列範例會使用 `STConvexHull()` 來尋找非凸面 `Polygon` 執行個體的凸面。  
  
```  
 DECLARE @g geography;  
 SET @g = geography::Parse('POLYGON((-120.533 46.566, -118.283 46.1, -122.3 47.45, -120.533 46.566))');  
 SELECT @g.STConvexHull().ToString();  
```  
  
### <a name="d-finding-the-convex-hull-on-a-geography-instance-with-an-envelope-angle-larger-than-90-degrees"></a>D. 尋找封套角度大於 90 度之 geography 執行個體上的凸面  
 下列範例會使用`STConvexHull()`上**geography**封套角度大於 90 度的執行個體。  
  
```
 DECLARE @g geography = 'POLYGON((20.533 46.566, -18.283 46.1, -22.3 47.45, 20.533 46.566))';  
 SELECT @g.STConvexHull().ToString();
 ```  
  
  

