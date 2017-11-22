---
title: "NumRings (geography 資料類型) |Microsoft 文件"
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
f1_keywords:
- NumRings_TSQL
- NumRings
dev_langs: TSQL
helpviewer_keywords: NumRings method
ms.assetid: 0e4e4fa2-b608-4cc4-98ba-0845ddb4214c
caps.latest.revision: "14"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4816f581690b5d68d970310a406de3f48ddb4fff
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="numrings-geography-data-type"></a>NumRings (geography 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  傳回中的環形總數**多邊形**執行個體。 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **geography**類型，外部和內部環形不會區別，因為任何環形可以採取來當做外部環形。  
  
## <a name="syntax"></a>語法  
  
```  
  
.NumRings ()  
```  
  
## <a name="return-type"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回型別： **int**  
  
 CLR 傳回類型： **SqlInt32**  
  
## <a name="remarks"></a>備註  
 這個方法會傳回 NULL，如果這不是**多邊形**執行個體，並會傳回 0，如果是空的執行個體。 這個方法是精確的。  
  
## <a name="examples"></a>範例  
 這個範例會建立具有兩個環形的 `Polygon` 例項，並確認它確實有兩個環形。  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653), (-122.357 47.654, -122.357 47.657, -122.349 47.657, -122.349 47.650, -122.357 47.654))', 4326);  
SELECT @g.NumRings();  
```  
  
## <a name="see-also"></a>請參閱＜  
 [地理例項上擴充的方法](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
