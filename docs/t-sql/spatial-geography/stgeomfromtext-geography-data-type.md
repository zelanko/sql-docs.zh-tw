---
title: "STGeomFromText (geography 資料類型) |Microsoft 文件"
ms.custom: 
ms.date: 07/30/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STGeomFromText (geography Data Type)
- STGeomFromText_TSQL
dev_langs: TSQL
helpviewer_keywords:
- full globe
- STGeomFromText method
ms.assetid: 3717987b-77d8-4ccf-a1db-5a8016ac1083
caps.latest.revision: "17"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: e781cdd50bd10711d181318cb584f6949828e19d
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="stgeomfromtext-geography-data-type"></a>STGeomFromText (geography 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

傳回**geography**執行個體所執行的執行個體夾帶任何 Z （高度） 和 M （測量） 值的開放式地理空間協會 (OGC) 已知文字 (well-known text，WKT) 表示法。
  
這**geography**資料類型方法可支援**FullGlobe**執行個體或大於半球的空間執行個體。
  
## <a name="syntax"></a>語法  
  
```  
  
STGeomFromText ( 'geography_tagged_text' , SRID )  
```  
  
## <a name="arguments"></a>引數  
 *geography_tagged_text*  
 是的 WKT 表示法**geography**来傳回執行個體。 *geography_tagged_text*是**nvarchar （max)**運算式。  
  
 *SRID*  
 是**int**運算式，表示的空間參考識別碼 (SRID) 的**geography**来傳回執行個體。  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回型別：**地理位置**  
  
 CLR 傳回類型： **SqlGeography**  
  
## <a name="remarks"></a>備註  
 OGC 類型**geography** Stgeomfromtext 所傳回的執行個體設定為對應的 WKT 輸入。  
  
 這個方法會擲回**ArgumentException**如果輸入包含對蹠邊緣。  
  
## <a name="examples"></a>範例  
 下列範例會使用 `STGeomFromText()` 建立 `geography` 例項。  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>請參閱＜  
 [OGC 靜態地理方法](../../t-sql/spatial-geography/ogc-static-geography-methods.md)  
  
  
