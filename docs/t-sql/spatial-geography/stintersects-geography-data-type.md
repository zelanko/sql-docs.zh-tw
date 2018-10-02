---
title: STIntersects (geography 資料型別) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STIntersects (geography Data Type)
- STIntersects_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STIntersects method
ms.assetid: c9db8b42-83c7-48c6-8963-fce54eb34c05
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 617edb15f042478982f62846947fad5caf5a0714
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47740236"
---
# <a name="stintersects-geography-data-type"></a>STIntersects (geography 資料類型)
[!INCLUDE[tsql-appliesto-ss2012-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-asdw-xxx-md.md)]

  如果 **geography** 執行個體與另一個 **geography** 執行個體相交，則會傳回 1。 如果不是則傳回 0。  
  
## <a name="syntax"></a>語法  
  
```  
  
.STIntersects ( other_geography )  
```  
  
## <a name="arguments"></a>引數  
 *other_geography*  
 這是要與 `STIntersects()` 叫用所在的執行個體相比較的另一個 **geography** 執行個體。  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**bit**  
  
 CLR 傳回類型：**SqlBoolean**  
  
## <a name="remarks"></a>Remarks  
 如果 **geography** 執行個體的空間參考識別碼 (SRID) 不相符，這個方法一定會傳回 **NULL**。  
  
## <a name="examples"></a>範例  
 下列範例使用 `STIntersects()` 來判斷兩個 `geography` 執行個體是否相交。  
  
```  
 DECLARE @g geography;  
 DECLARE @h geography;  
 SET @g = geography::STGeomFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))', 4326);  
 SET @h = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
```  
  
 ```
 SELECT CASE @g.STIntersects(@h) 
 WHEN 1 THEN '@g intersects @h'  
 ELSE '@g does not intersect @h'  
 END;
 ```  
  
## <a name="see-also"></a>另請參閱  
 [地理例項上的 OGC 方法](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
