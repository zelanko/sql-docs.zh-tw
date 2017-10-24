---
title: "STPolyFromText (geography 資料類型) |Microsoft 文件"
ms.custom: 
ms.date: 07/30/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STPolyFromText_TSQL
- STPolyFromText (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STPolyFromText method
ms.assetid: d7e6a2bb-d301-49fb-9202-c70a9d169b4d
caps.latest.revision: 13
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b33eef062e4a72cb84c077979de7717a10fdc3a3
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="stpolyfromtext-geography-data-type"></a>STPolyFromText (geography 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

傳回**geography**執行個體所執行的執行個體夾帶任何 Z （高度） 和 M （測量） 值的開放式地理空間協會 (OGC) 已知文字 (well-known text，WKT) 表示法。
  
## <a name="syntax"></a>語法  
  
```  
  
STPolyFromText ( 'polygon_tagged_text' , SRID )  
```  
  
## <a name="arguments"></a>引數  
 *polygon_tagged_text*  
 是的 WKT 表示法**geographyPolygon**您想要傳回的執行個體。 *polygon_tagged_text*是**nvarchar （max)**運算式。  
  
 *SRID*  
 是**int**運算式，表示的空間參考識別碼 (SRID) 的**geographyPolygon**您想要傳回的執行個體。  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回型別：**地理位置**  
  
 CLR 傳回類型： **SqlGeography**  
  
 OGC 類型：**多邊形**  
  
## <a name="remarks"></a>備註  
 這個方法會擲回**FormatException**如果輸入格式不正確。  
  
## <a name="examples"></a>範例  
 下列範例會使用 `STPolyFromText()` 建立 `geography` 例項。  
  
```  
DECLARE @g geography;  
SET @g = geography::STPolyFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))', 4326);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>另請參閱  
 [OGC 靜態地理方法](../../t-sql/spatial-geography/ogc-static-geography-methods.md)  
  
  

