---
description: STIsSimple (geometry 資料類型)
title: STIsSimple (geometry 資料型別) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STIsSimple_TSQL
- STIsSimple (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STIsSimple (geometry Data Type)
ms.assetid: da8f45d4-4f9c-405d-b883-760eb5344a71
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 51e9f38a40b26ab4ff50c371519ed50e85ae984d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88472450"
---
# <a name="stissimple-geometry-data-type"></a>STIsSimple (geometry 資料類型)
[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

如果 **geometry** 執行個體是簡單的執行個體 (如開放地理空間協會 (Open Geospatial Consortium，OGC) 所定義)，就會傳回 1。 如果 **geometry** 執行個體不是簡單的執行個體，就會傳回 0。
  
## <a name="syntax"></a>語法  
  
```  
  
.STIsSimple ( )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>傳回型別
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**bit**  
  
 CLR 傳回類型：**SqlBoolean**  
  
## <a name="remarks"></a>備註  
 **geometry** 執行個體必須符合以下所有的需求，才能是簡單的執行個體：  
  
-   此例項的每一個圖形都不能自己相交 (除了在它的端點上以外)。  
  
-   此例項的兩個圖形不能在非兩者界限內的點上彼此相交。  
  
## <a name="examples"></a>範例  
 下列範例會建立與自己相交的非簡單式 `LineString` 例項，並使用 `STIsSimple()` 來測試看看 `LineString` 是否為簡單的例項。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 0 2, 2 0)', 0);  
SELECT @g.STIsSimple();  
```  
  
## <a name="see-also"></a>另請參閱  
 [幾何例項上的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

