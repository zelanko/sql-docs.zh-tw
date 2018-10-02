---
title: STConvexHull (geography 資料型別) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- STConvexHull method (geography)
ms.assetid: fb435db7-31bb-4243-9d8b-35379184cfb4
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 6f44a22b200eba0948ceb1bd036d51ceff884442
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47666856"
---
# <a name="stconvexhull-geography-data-type"></a>STConvexHull (geography 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  傳回物件，表示 **geography** 執行個體的凸殼。  
  
## <a name="syntax"></a>語法  
  
```  
  
.STConvexHull ( )  
```  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**geography**  
  
 CLR 傳回類型：**SqlGeography**  
  
## <a name="remarks"></a>Remarks  
 針對封套角度大於 90 度的 **geography** 執行個體傳回 `FullGlobe` 物件。  
  
 針對空白 **geography** 執行個體傳回空白 **geography** 集合。  
  
 針對未初始化的 **geography** 執行個體傳回 **null**。  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-stconvexhull-on-an-uninitialized-geography-instance"></a>A. 在未初始化的 geography 執行個體上使用 STConvexHull()  
 下列範例會在未初始化的 **geography** 執行個體上使用 `STConvexHull()`。  
  
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
 下列範例會在封套角度大於 90 度的 **geography** 執行個體上使用 `STConvexHull()`。  
  
```
 DECLARE @g geography = 'POLYGON((20.533 46.566, -18.283 46.1, -22.3 47.45, 20.533 46.566))';  
 SELECT @g.STConvexHull().ToString();
 ```  
  
  
