---
title: STMPolyFromText (geometry 資料類型) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STMPolyFromText (geometry Data Type)
- STMPolyFromText_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STMPolyFromText (geometry Data Type)
ms.assetid: f087a61c-f063-4fb8-8f1c-251a2fed76a1
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 015de9248eb9e3af834a2c595abc8efdc2fc3794
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/21/2020
ms.locfileid: "86554973"
---
# <a name="stmpolyfromtext-geometry-data-type"></a>STMPolyFromText (geometry 資料類型)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

從「開放地理空間協會」(OGC) 的「已知文字」(WKT) 表示法傳回 **geometry** 執行個體 (附帶此執行個體所攜帶的任何 Z (高度) 和 M (測量) 值)。
  
## <a name="syntax"></a>語法  
  
```  
  
STMPolyFromText ( 'multipolygon_tagged_text' , SRID )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引數
 *multipolygon_tagged_text*  
 這是要傳回之 **geometryMultiPolygon** 執行個體的 WKT 表示法。 *multipolygon_tagged_text* 是 **nvarchar(max)** 運算式。  
  
 *SRID*  
 這是 **int** 運算式，代表要傳回之 **geometryMultiPolygon** 執行個體的空間參考識別碼 (SRID)。  
  
## <a name="return-types"></a>傳回型別  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**geometry**  
  
 CLR 傳回類型：**Sql Geometry**  
  
 OGC 類型：**MultiPolygon**  
  
## <a name="remarks"></a>備註  
 如果輸入的格式不正確，這個方法將會擲回 **FormatException**。  
  
## <a name="examples"></a>範例  
 下列範例會使用 `STMPolyFromText()` 建立 `geometry` 例項。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STMPolyFromText('MULTIPOLYGON (((5 5, 10 5, 10 10, 5 5)), ((10 10, 100 10, 200 200, 30 30, 10 10)))', 0);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>另請參閱  
 [OGC 靜態幾何方法](../../t-sql/spatial-geometry/ogc-static-geometry-methods.md)  
  
  

