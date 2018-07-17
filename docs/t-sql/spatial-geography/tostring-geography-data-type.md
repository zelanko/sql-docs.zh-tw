---
title: ToString (geography 資料類型) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ToString (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- ToString method
ms.assetid: 045c12fa-8fc6-441a-9500-7021cb4ff13e
caps.latest.revision: 18
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 3374a55d457818ec859a1f0d1c9644a05bccab8f
ms.sourcegitcommit: a6596c62f607041c4402f7d5b41a232fca257c14
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36250020"
---
# <a name="tostring-geography-data-type"></a>ToString (geography 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  傳回開放地理空間協會 (Open Geospatial Consortium，OGC) 對於 **geography** 執行個體的已知的文字 (Well-Known Text，WKT) 表示法，經由此執行個體夾帶的任何 Z (高度) 和 M (測量) 值來擴充。  
  
 這個 geography 資料類型方法可支援 **FullGlobe** 執行個體或大於半球的空間執行個體。  
  
## <a name="syntax"></a>語法  
  
```  
  
.ToString ()  
```  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**nvarchar(max)**  
  
 CLR 傳回類型：**SqlString**  
  
## <a name="remarks"></a>Remarks  
 這個方法在 Null 執行個體上呼叫時，將會傳回 "Null" 字串。 在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 中，伺服器上的可能結果集已擴充到 **FullGlobe** 執行個體。 這個方法會傳回與 `AsTextZM()` 相同的值。  
  
 這個方法並不精確。  
  
## <a name="examples"></a>範例  
 下列範例會建立 `LineString` 執行個體，並使用 `ToString()` 傳回此執行個體的文字描述。  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>另請參閱  
 [地理執行個體上擴充的方法](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [AsTextZM &#40;geography 資料類型&#41;](../../t-sql/spatial-geography/astextzm-geography-data-type.md)  
  
  
