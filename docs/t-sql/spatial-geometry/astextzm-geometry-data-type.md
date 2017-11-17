---
title: "AsTextZM (geometry 資料類型) |Microsoft 文件"
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
- AsTextZM_TSQL
- AsTextZM
- AsTextZM (geometry Data Type)
- AsTextZM_(geometry_Data_Type)_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- AsTextZM (geometry Data Type)
ms.assetid: 08ac8aa0-aff7-4b22-87e0-1a1d55dcbc04
caps.latest.revision: 20
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 91f77bd684d79bbef2530307aa65fc0d92b91c5e
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="astextzm-geometry-data-type"></a>AsTextZM (geometry 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

傳回開放式地理空間協會 (OGC) 已知文字 (well-known text，WKT) 表示法的 geometry 執行個體夾帶任何**Z** （高度） 和**M** （測量） 值執行個體所夾帶。
  
## <a name="syntax"></a>語法  
  
```  
  
.AsTextZM ()  
```  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回型別： **nvarchar （max)**  
  
 CLR 傳回類型： **SqlChars**  
  
## <a name="remarks"></a>備註  
  
## <a name="examples"></a>範例  
 下列範例會建立`Point`包含執行個體**Z** （高度） 和**M** （測量） 值。 `STAsText()`會選取 WKT 值 (1 2);`AsTextZM()`選取相同的 WKT 值，也會傳回的值**Z**和**M**，產生 (1 2 3 4)。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POINT(1 2 3 4)', 0);  
SELECT @g.STAsText();  
SELECT @g.AsTextZM();  
```  
  
## <a name="see-also"></a>另請參閱  
 [幾何例項上擴充的方法](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)   
 [M &#40; geometry 資料類型 &#41;](../../t-sql/spatial-geometry/m-geometry-data-type.md)   
 [Z &#40; geometry 資料類型 &#41;](../../t-sql/spatial-geometry/z-geometry-data-type.md)  
  
  


