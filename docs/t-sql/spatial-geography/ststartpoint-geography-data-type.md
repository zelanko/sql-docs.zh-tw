---
title: STStartPoint (geography 資料類型) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STStartPoint_TSQL
- STStartPoint (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STStartPoint method
ms.assetid: 7df18a5f-b9ee-4e36-b765-a0790c1dee3d
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 80b78fbd1aff4490ae71198bc86b26926448f6f4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47615926"
---
# <a name="ststartpoint-geography-data-type"></a>STStartPoint (geography 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  傳回 **geography** 執行個體的起點。  
  
## <a name="syntax"></a>語法  
  
```  
  
.STStartPoint ( )  
```  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**geography**  
  
 CLR 傳回類型：**SqlGeography**  
  
 開放地理空間協會 (OGC) 類型：**Point**  
  
## <a name="remarks"></a>Remarks  
 STStartPoint() 相當於 [STPointN](../../t-sql/spatial-geometry/stpointn-geometry-data-type.md)`(1)`。  
  
## <a name="examples"></a>範例  
 下列範例會建立 `LineString` 例項，並使用 `STStartPoint()` 來擷取此例項的起點。  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STStartPoint().ToString();  
```  
  
## <a name="see-also"></a>另請參閱  
 [地理例項上的 OGC 方法](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
