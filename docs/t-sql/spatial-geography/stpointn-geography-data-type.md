---
title: "STPointN (geography 資料類型) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STPointN_TSQL
- STPointN (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STPointN method
ms.assetid: 47670feb-b9e0-4b4b-af83-b9bba7da66ac
caps.latest.revision: 15
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 15a196cf9ac1c5f560a2eeee3d0262829f88480b
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="stpointn-geography-data-type"></a>STPointN (geography 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  傳回在指定的點**geography**執行個體。  
  
## <a name="syntax"></a>語法  
  
```  
  
.STPointN ( expression )  
```  
  
## <a name="arguments"></a>引數  
 *expression*  
 是**int**介於 1 到中點數目的運算式**geography**執行個體。  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回型別：**地理位置**  
  
 CLR 傳回類型： **SqlGeography**  
  
 開放式地理空間協會 (OGC) 類型：**點**  
  
## <a name="remarks"></a>備註  
 如果**geography**執行個體是使用者所建立，STPointN() 會傳回所指定的點*運算式*由所在它們根據原來輸入的順序排序這些點。  
  
 如果**geography**執行個體由系統所建構，STPointN() 會傳回所指定的點*運算式*由相同的順序排序這些點，其方式是輸出： 首先是根據**geography**執行個體，再根據環形內的執行個體 （如果適用），然後再根據環形內的點。 這個順序具決定性。  
  
 如果使用小於 1 的值呼叫此方法時，它會擲回**ArgumentOutOfRangeException**。  
  
 如果使用大於例項中點數的值來呼叫此方法，它會傳回 Null。  
  
## <a name="examples"></a>範例  
 下列範例會建立 `LineString` 例項，並使用 `STPointN()` 來擷取例項描述中的第二個點。  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STPointN(2).ToString();  
```  
  
## <a name="see-also"></a>另請參閱  
 [Geography 執行個體上的 OGC 方法](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
