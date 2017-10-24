---
title: "STLineFromText (geometry 資料類型) |Microsoft 文件"
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STLineFromText (geometry Data Type)
- STLineFromText_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STLineFromText (geometry Data Type)
ms.assetid: 430508ad-207b-4dee-a4d1-4ddf25e6b4a9
caps.latest.revision: 20
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: cb1596629f30ff936bd53afd54affc3321f4e53c
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="stlinefromtext-geometry-data-type"></a>STLineFromText (geometry 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

傳回**幾何**執行個體所執行的執行個體夾帶任何 Z （高度） 和 M （測量） 值的開放式地理空間協會 (OGC) 已知文字 (well-known text，WKT) 表示法。
  
## <a name="syntax"></a>語法  
  
```  
  
STLineFromText ( 'linestring_tagged_text' , SRID )  
```  
  
## <a name="arguments"></a>引數  
 *linestring_tagged_text*  
 是的 WKT 表示法**geometryLineString**您想要傳回的執行個體。 *linestring_tagged_text*是**nvarchar （max)**運算式。  
  
 *SRID*  
 是**int**運算式，表示的空間參考識別碼 (SRID) 的**geometryLineString**您想要傳回的執行個體。  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回型別：**幾何**  
  
 CLR 傳回類型： **SqlGeometry**  
  
 OGC 類型： **LineString**  
  
## <a name="remarks"></a>備註  
 這個方法會擲回**FormatException**如果輸入格式不正確。  
  
## <a name="examples"></a>範例  
 下列範例會使用 `STLineFromText()` 建立 `geometry` 例項。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STLineFromText('LINESTRING (100 100, 200 200)', 0);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>另請參閱  
 [OGC 靜態幾何方法](../../t-sql/spatial-geometry/ogc-static-geometry-methods.md)  
  
  


