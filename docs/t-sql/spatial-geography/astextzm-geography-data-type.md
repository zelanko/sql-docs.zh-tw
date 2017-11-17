---
title: "AsTextZM (geography 資料類型) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
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
- AsTextZM (geography Data Type)
- AsTextZM_TSQL
- AsTextZM
- AsTextZM_(geography_Data_Type)_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- AsTextZM method
ms.assetid: e9dc27f6-e945-4457-8498-7644db34008e
caps.latest.revision: 14
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ba824c4482f49d534d11666054a0a8d3a1669d2d
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="astextzm-geography-data-type"></a>AsTextZM (geography 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  傳回開放式地理空間協會 (OGC) 已知文字 (well-known text，WKT) 表示**geography**執行個體夾帶任何**Z** （高度） 和**M** （量值）執行個體所夾帶的值。  
  
## <a name="syntax"></a>語法  
  
```  
  
.AsTextZM ()  
```  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回型別： **nvarchar （max)**  
  
 CLR 傳回類型： **SqlChars**  
  
## <a name="remarks"></a>備註  
  
## <a name="examples"></a>範例  
 下列範例會建立`Point`包含執行個體**Z** （高度） 和**M** （測量） 值。 `STAsText()`會選取 WKT 值 (-122.34900 47.65100);`AsTextZM()`選取相同的 WKT 值，也會傳回的值**Z**和**M**，產生 (-122.34900 47.65100 10.3 12)。  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POINT(-122.34900 47.65100 10.3 12)', 4326);  
SELECT @g.STAsText();  
SELECT @g.AsTextZM();  
```  
  
## <a name="see-also"></a>另請參閱  
 [Geography 執行個體上的擴充的方法](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [M &#40; geography 資料類型 &#41;](../../t-sql/spatial-geography/m-geography-data-type.md)   
 [Z &#40; geography 資料類型 &#41;](../../t-sql/spatial-geography/z-geography-data-type.md)  
  
  

