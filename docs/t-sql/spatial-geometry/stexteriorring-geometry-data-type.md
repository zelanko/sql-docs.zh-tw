---
title: STExteriorRing (geometry 資料型別) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- STExteriorRing_TSQL
- STExteriorRing (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STExteriorRing (geometry Data Type)
ms.assetid: b402b36f-05bf-4c6d-8cd6-76c0fff19db2
caps.latest.revision: 20
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f32dd16ea4fb782aa6f2ca5824d1662c45d16ff8
ms.sourcegitcommit: a6596c62f607041c4402f7d5b41a232fca257c14
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36239512"
---
# <a name="stexteriorring-geometry-data-type"></a>STExteriorRing (geometry 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

傳回多邊形 **geometry** 執行個體的外環。
  
## <a name="syntax"></a>語法  
  
```  
  
.STExteriorRing ( )  
```  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**geometry**  
  
 CLR 傳回類型：**SqlGeometry**  
  
 開放地理空間協會 (OGC) 類型：**LineString**  
  
## <a name="remarks"></a>Remarks  
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
  
  

