---
title: NumRings (geography 資料型別) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- NumRings_TSQL
- NumRings
dev_langs:
- TSQL
helpviewer_keywords:
- NumRings method
ms.assetid: 0e4e4fa2-b608-4cc4-98ba-0845ddb4214c
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: ad07cdaffd8e7cd207691e218ad8eaabf293b0db
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65937549"
---
# <a name="numrings-geography-data-type"></a>NumRings (geography 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  傳回 **Polygon** 執行個體中的環形總數。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **geography** 型別中，不會區分外部和內部環形，因為任何環形都可以當做外部環形。  
  
## <a name="syntax"></a>語法  
  
```  
  
.NumRings ()  
```  
  
## <a name="return-type"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**int**  
  
 CLR 傳回型別：**SqlInt32**  
  
## <a name="remarks"></a>Remarks  
 如果這不是 **Polygon** 執行個體，這個方法將會傳回 NULL；如果此執行個體是空的，則會傳回 0。 這個方法是精確的。  
  
## <a name="examples"></a>範例  
 這個範例會建立具有兩個環形的 `Polygon` 例項，並確認它確實有兩個環形。  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653), (-122.357 47.654, -122.357 47.657, -122.349 47.657, -122.349 47.650, -122.357 47.654))', 4326);  
SELECT @g.NumRings();  
```  
  
## <a name="see-also"></a>另請參閱  
 [地理例項上擴充的方法](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
