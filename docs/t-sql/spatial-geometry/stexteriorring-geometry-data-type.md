---
title: STExteriorRing (geometry 資料型別) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STExteriorRing_TSQL
- STExteriorRing (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STExteriorRing (geometry Data Type)
ms.assetid: b402b36f-05bf-4c6d-8cd6-76c0fff19db2
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 2948e131d27437ca09fc11aee7d2d3805db7e372
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85762573"
---
# <a name="stexteriorring-geometry-data-type"></a>STExteriorRing (geometry 資料類型)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

傳回多邊形 **geometry** 執行個體的外環。
  
## <a name="syntax"></a>語法  
  
```  
  
.STExteriorRing ( )  
```  
  
## <a name="return-types"></a>傳回型別  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**geometry**  
  
 CLR 傳回類型：**SqlGeometry**  
  
 開放地理空間協會 (OGC) 類型：**LineString**  
  
## <a name="remarks"></a>備註  
 如果 **geometry** 執行個體不是多邊形，這個方法會傳回 **null**。  
  
## <a name="examples"></a>範例  
 下例範例會建立 `Polygon` 執行個體，並使用 `STExteriorRing()` 傳回 **LineString** 形式之多邊形的外環。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POLYGON((0 0, 3 0, 3 3, 0 3, 0 0),(2 2, 2 1, 1 1, 1 2, 2 2))', 0);  
SELECT @g.STExteriorRing().ToString();  
```  
  
## <a name="see-also"></a>另請參閱  
 [幾何例項上的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

