---
description: STAsBinary (geography 資料類型)
title: STAsBinary (geography 資料型別) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STAsBinary_TSQL
- STAsBinary (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STAsBinary method
ms.assetid: 99602a62-265d-4aa4-a8dc-92992ca55ba4
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 7ae9c800cffd7df80ba8447c2e16de745a0009bc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88359444"
---
# <a name="stasbinary-geography-data-type"></a>STAsBinary (geography 資料類型)
[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

  傳回 **geography** 執行個體的開放地理空間協會 (OGC) 已知的二進位 (WKB) 表示法。  
  
 這個 **geography** 資料類型方法可支援 **FullGlobe** 執行個體或大於半球的空間執行個體。  
  
## <a name="syntax"></a>語法  
  
```  
  
.STAsBinary ( )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>傳回型別
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**varbinary(max)**  
  
 CLR 傳回類型：**SqlBytes**  
  
## <a name="remarks"></a>備註  
 可以叫用 [STGeometryType()](../../t-sql/spatial-geography/stgeometrytype-geography-data-type.md) 來判斷 **geography** 執行個體的 OGC 型別。  
  
## <a name="examples"></a>範例  
 下列範例使用 `STAsBinary()`，從文字建立 (-122.360, 47.656) 到 (-122.343, 47.656) 的 `LineString``geography` 執行個體。 然後，它會在 WKB 中傳回結果。  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING( -122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STAsBinary();  
```  
  
## <a name="see-also"></a>另請參閱  
 [地理位置例項上的 OGC 方法](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
