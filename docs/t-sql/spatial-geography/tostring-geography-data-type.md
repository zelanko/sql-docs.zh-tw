---
title: "ToString (geography 資料類型) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: ToString (geography Data Type)
dev_langs: TSQL
helpviewer_keywords: ToString method
ms.assetid: 045c12fa-8fc6-441a-9500-7021cb4ff13e
caps.latest.revision: "18"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bcec246b4358b3d8b59467975bb836ea226463ab
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="tostring-geography-data-type"></a>ToString (geography 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  傳回開放式地理空間協會 (OGC) 已知文字 (well-known text，WKT) 表示**geography**執行個體所執行的執行個體夾帶任何 Z （高度） 和 M （測量） 值。  
  
 這個 geography 資料類型方法可支援**FullGlobe**執行個體或大於半球的空間執行個體。  
  
## <a name="syntax"></a>語法  
  
```  
  
.ToString ()  
```  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回型別： **nvarchar （max)**  
  
 CLR 傳回類型： **SqlString**  
  
## <a name="remarks"></a>備註  
 這個方法在 Null 執行個體上呼叫時，將會傳回 "Null" 字串。 在[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]，伺服器上的可能結果集已擴充到**FullGlobe**執行個體。 這個方法會傳回與 `AsTextZM()` 相同的值。  
  
 這個方法並不精確。  
  
## <a name="examples"></a>範例  
 下列範例會建立`LineString`執行個體，並使用`ToString()`傳回執行個體的文字描述。  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>另請參閱  
 [Geography 執行個體上的擴充的方法](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [AsTextZM &#40;geography 資料類型&#41;](../../t-sql/spatial-geography/astextzm-geography-data-type.md)  
  
  
