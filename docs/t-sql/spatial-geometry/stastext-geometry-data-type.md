---
title: "STAsText (geometry 資料類型) |Microsoft 文件"
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 127e64908ad9cb768d31e3c1ec42988962289246
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="stastext-geometry-data-type"></a>STAsText (geometry 資料類型)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

傳回開放式地理空間協會 (OGC) 已知文字 (well-known text，WKT) 表示**幾何**執行個體。 此文字將不會包含此執行個體所夾帶的任何 Z (高度) 或 M (測量) 值。
  
## <a name="syntax"></a>語法  
  
```  
  
.STAsText ( )  
```  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回型別： **nvarchar （max)**  
  
 CLR 傳回類型： **SqlChars**  
  
## <a name="examples"></a>範例  
 下列範例會從文字建立 (0,0) 到 (2,3) 的 `LineString` 幾何例項。 `STAsText()` 會在文字中傳回結果。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 3)', 0);  
SELECT @g.STAsText();  
```  
  
## <a name="see-also"></a>另請參閱  
 [幾何例項上的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  


