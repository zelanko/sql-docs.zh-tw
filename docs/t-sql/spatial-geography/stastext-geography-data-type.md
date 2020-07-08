---
title: STAsText (geography y 資料型別) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STAsText (geography Data Type)
- STAsText_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STAsText method
ms.assetid: d3d2635d-ca6c-4205-9d6c-eb939ee314fd
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 207341d09f153ed819d331960cf00dbb6c410bf3
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85704954"
---
# <a name="stastext-geography-data-type"></a>STAsText (geography 資料類型)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  傳回 **geography** 執行個體的開放地理空間協會 (OGC) 已知的文字 (WKT) 表示法。 此文字將不會包含此執行個體所夾帶的任何 Z (高度) 或 M (測量) 值。  
  
 這個 **geography** 資料類型方法可支援 **FullGlobe** 執行個體或大於半球的空間執行個體。  
  
## <a name="syntax"></a>語法  
  
```  
  
.STAsText ( )  
```  
  
## <a name="return-types"></a>傳回型別  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**nvarchar(max)**  
  
 CLR 傳回類型：**SqlChars**  
  
## <a name="remarks"></a>備註  
 可以叫用 [STGeometryType()](../../t-sql/spatial-geography/stgeometrytype-geography-data-type.md) 來判斷 **geography** 執行個體的 OGC 型別。  
  
 在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 中，伺服器上傳回的可能結果集已擴充到 **FullGlobe** 執行個體。  
  
## <a name="examples"></a>範例  
 下列範例使用 `STAsText()`，從文字建立 (-122.360, 47.656) 到 (-122.343, 47.656) 的 `LineString``geography` 執行個體。 然後，它會在文字中傳回結果。  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STAsText();  
```  
  
## <a name="see-also"></a>另請參閱  
 [地理例項上的 OGC 方法](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
