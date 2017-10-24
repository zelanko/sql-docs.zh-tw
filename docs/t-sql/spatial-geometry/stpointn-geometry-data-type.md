---
title: "STPointN (geometry 資料類型) |Microsoft 文件"
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STPointN_TSQL
- STPointN (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STPointN (geometry Data Type)
ms.assetid: 8f0bb3b7-5cd9-42c2-b9f8-f04628653bd0
caps.latest.revision: 22
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d6e46115d41a0a1b717502ed8475884268ea1af0
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="stpointn-geometry-data-type"></a>STPointN (geometry 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

傳回在指定的點**幾何**執行個體。
  
## <a name="syntax"></a>語法  
  
```  
  
.STPointN ( expression )  
```  
  
## <a name="arguments"></a>引數  
 *expression*  
 是**int**介於 1 到中點數目的運算式**幾何**執行個體。  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回型別：**幾何**  
  
 CLR 傳回類型： **SqlGeometry**  
  
 開放式地理空間協會 (OGC) 類型：**點**  
  
## <a name="remarks"></a>備註  
 如果**幾何**執行個體是使用者所建立，`STPointN()`傳回所指定的點*運算式*由所在它們根據原來輸入的順序排序這些點。  
  
 如果**幾何**建構執行個體時，系統`STPointN()`傳回所指定的點*運算式*由相同的順序排序這些點，其方式是輸出： 首先是根據幾何，然後是由環形內的幾何 （如果適用），然後再由環形內的點。 這個順序具決定性。  
  
 如果使用小於 1 的值呼叫此方法時，它會擲回**ArgumentOutOfRangeException**。  
  
 如果使用大於例項中點數的值來呼叫此方法，它會傳回 Null。  
  
## <a name="examples"></a>範例  
 下列範例會建立 `LineString` 例項，並使用 `STPointN()` 來擷取例項描述中的第二個點。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 1 0)', 0);  
SELECT @g.STPointN(2).ToString();  
```  
  
## <a name="see-also"></a>另請參閱  
 [幾何例項上的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  


