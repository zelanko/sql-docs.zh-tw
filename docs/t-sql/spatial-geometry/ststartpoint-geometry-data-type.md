---
description: STStartPoint (geometry 資料類型)
title: STStartPoint (geometry 資料類型) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STStartPoint_TSQL
- STStartPoint (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STStartPoint (geometry Data Type)
ms.assetid: 049917db-3f76-4053-8cd2-bc54158e89bc
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 3fd64405d2e08038701262105675557893cdf96f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88416854"
---
# <a name="ststartpoint-geometry-data-type"></a>STStartPoint (geometry 資料類型)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

傳回 **geometry** 執行個體的起點。
  
## <a name="syntax"></a>語法  
  
```  
  
.STStartPoint ( )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>傳回型別
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**geometry**  
  
 CLR 傳回類型：**SqlGeometry**  
  
 開放地理空間協會 (OGC) 類型：**Point**  
  
## <a name="remarks"></a>備註  
 `STStartPoint()` 等同於 [STPointN](../../t-sql/spatial-geometry/stpointn-geometry-data-type.md) (1)。  
  
## <a name="examples"></a>範例  
 下列範例會建立 `LineString` 例項，並使用 `STStartPoint()` 來擷取此例項的起點。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 1 0)', 0);  
SELECT @g.STStartPoint().ToString();  
```  
  
## <a name="see-also"></a>另請參閱  
 [STPointN &#40;geometry 資料類型&#41;](../../t-sql/spatial-geometry/stpointn-geometry-data-type.md)   
 [幾何例項上的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

