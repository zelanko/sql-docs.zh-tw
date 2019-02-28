---
title: STGeomCollFromWKB (geometry 資料類型) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STGeomCollFromWKB (geometry Data Type)
- STGeomCollFromWKB_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STGeomCollFromWKB (geometry Data Type)
ms.assetid: 6c55032c-7f5e-4181-8e67-c0265032db63
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 5693d4673cc589507e7dde73dbdf68198a03cf0e
ms.sourcegitcommit: 009bee6f66142c48477849ee03d5177bcc3b6380
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/13/2019
ms.locfileid: "56230935"
---
# <a name="stgeomcollfromwkb-geometry-data-type"></a>STGeomCollFromWKB (geometry 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

從「開放地理空間協會」(OGC) 的「已知二進位」(WKB) 表示法傳回 **geometrycollection** 執行個體。
  
## <a name="syntax"></a>語法  
  
```  
  
STGeomCollFromWKB ( 'WKB_geometrycollection' , SRID )  
```  
  
## <a name="arguments"></a>引數  
 *WKB_geometrycollection*  
 這是要傳回之 **geometrycollection** 執行個體的 WKB 表示法。 *WKB_geometrycollection* 是 **varbinary(max)** 運算式。  
  
 *SRID*  
 這是 **int** 運算式，代表要傳回之 **geometry** 執行個體的空間參考識別碼 (SRID)。  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**geometry**  
  
 CLR 傳回類型：**SqlGeometry**  
  
## <a name="remarks"></a>Remarks  
 `STGeomCollFromWKB()` 所傳回之 **geometry** 執行個體的 OGC 類型會根據對應的 WKB 輸入，設定為 **GeomCollection**、**MultiPolygon**、**MultiLineString** 或 **MultiPoint**。  
  
 如果輸入的格式不正確，這個方法將會擲回 FormatException 例外狀況。  
  
## <a name="examples"></a>範例  
 下列範例會使用 `STGeomCollFromWKB()` 來建立 **geometry** 執行個體。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomCollFromWKB(0x0107000000020000000103000000010000000400000000000000000014400000000000001440000000000000244000000000000014400000000000002440000000000000244000000000000014400000000000001440010100000000000000000024400000000000002440, 0);  
SELECT @g.STAsText();  
```  
  
## <a name="see-also"></a>另請參閱  
 [OGC 靜態幾何方法](../../t-sql/spatial-geometry/ogc-static-geometry-methods.md)  
  
