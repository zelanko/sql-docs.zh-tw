---
title: STNumCurves (geography 資料類型) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|spatial-geography
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- STNumCurves
- STNumCurves_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STNumCurves method (geography)
ms.assetid: e98a56c2-8496-4dfd-9b37-7f3c4ca9b2b5
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e2acda5ed4fa89dbda902b64afec541d38ba3b84
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "33060915"
---
# <a name="stnumcurves-geography-data-type"></a>STNumCurves (geography 資料類型)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  傳回一維 **geography** 執行個體中的曲線數目。  
  
## <a name="syntax"></a>語法  
  
```  
  
.STNumCurves()  
```  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**geography**  
  
 CLR 傳回類型：**SqlGeography**  
  
## <a name="remarks"></a>Remarks  
 一維空間資料類型包括 **LineString**、**CircularString** 及 **CompoundCurve**。 空的一維 **geography** 執行個體會傳回 0。  
  
 `STNumCurves`() 只在簡單類型上運作；它不能與 **geography**集合 (如 **MultiLineString**) 搭配使用。 當 **geography** 執行個體不是一維資料類型時，會傳回 **NULL**。  
  
 針對未初始化的 **geography** 執行個體傳回 **Null**。  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-stnumcurves-on-a-circularstring-instance"></a>A. 在 CircularString 執行個體上使用 STNumCurves()  
 下列範例會顯示如何取得 `CircularString` 執行個體中的曲線數目：  
  
```
 DECLARE @g geography; 
 SET @g = geography::Parse('CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)');  
 SELECT @g.STNumCurves();
 ```  
  
### <a name="b-using-stnumcurves-on-a-compoundcurve-instance"></a>B. 在 CompoundCurve 執行個體上使用 STNumCurves()  
 下列範例會使用 `STNumCurves()` 傳回 `CompoundCurve` 執行個體中的曲線數目。  
  
```
 DECLARE @g geography;  
 SET @g = geography::Parse('COMPOUNDCURVE(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))');  
 SELECT @g.STNumCurves();
 ```  
  
## <a name="see-also"></a>另請參閱  
 [空間資料類型概觀](../../relational-databases/spatial/spatial-data-types-overview.md)   
 [地理例項上的 OGC 方法](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
