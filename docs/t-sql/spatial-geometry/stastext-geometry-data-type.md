---
title: STAsText (geometry 資料型別) | Microsoft Docs
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
- STAsText_TSQL
- STAsText (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STAsText (geometry Data Type)
ms.assetid: e0decf5e-2858-4c56-b61a-6123f47fb51c
caps.latest.revision: 25
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e1d7b80cd26cc424dcc21ed2f545e9e6deeb64f7
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "37997230"
---
# <a name="stastext-geometry-data-type"></a>STAsText (geometry 資料類型)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

傳回 **geometry** 執行個體的開放地理空間協會 (Open Geospatial Consortium，OGC) 已知的文字 (Well-Known Text，WKT) 表示法。 此文字將不會包含此執行個體所夾帶的任何 Z (高度) 或 M (測量) 值。
  
## <a name="syntax"></a>語法  
  
```  
  
.STAsText ( )  
```  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**nvarchar(max)**  
  
 CLR 傳回類型：**SqlChars**  
  
## <a name="examples"></a>範例  
 下列範例會從文字建立 (0,0) 到 (2,3) 的 `LineString` 幾何例項。 `STAsText()` 會在文字中傳回結果。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 3)', 0);  
SELECT @g.STAsText();  
```  
  
## <a name="see-also"></a>另請參閱  
 [幾何例項上的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

