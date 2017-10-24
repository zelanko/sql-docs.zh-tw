---
title: "STCurveToLine (geography 資料類型) |Microsoft 文件"
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
- STCurveToLine_TSQL
- STCurveToLine
dev_langs:
- TSQL
helpviewer_keywords:
- STCurveToLine method (geography)
ms.assetid: 2f863a85-6168-465a-b32f-bb5e3de58dee
caps.latest.revision: 12
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9d2ad93d8bc292ebb86233917dc3f934fbe57dca
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="stcurvetoline-geography-data-type"></a>STCurveToLine (geography 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  傳回的多邊形近似值**geography**包含圓弧線段的執行個體。  
  
## <a name="syntax"></a>語法  
  
```  
  
.STCurveToLine()  
```  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回型別：**地理位置**  
  
 CLR 傳回類型： **SqlGeography**  
  
## <a name="remarks"></a>備註  
 傳回**LineString**例項而言**CircularString**或**CompoundCurve**執行個體。  
  
 傳回**多邊形**例項而言**CurvePolygon**執行個體。  
  
 傳回一份**geography**不包含的執行個體**CircularString**， **CompoundCurve**，或**CurvePolygon**執行個體。  
  
 不同於 SQL MM 規格，這個方法不會使用計算多邊形近似值的 z 座標值。 呼叫中出現的任何 z 座標值**geography**執行個體都會被忽略。  
  
## <a name="examples"></a>範例  
 下列範例會傳回 `LineString` 執行個體，這是 `CircularString` 執行個體的多邊形近似值：  
  
```
 DECLARE @g1 geography = 'CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
 DECLARE @g2 geography;  
 SET @g2 = @g1.STCurveToLine();  
 SELECT @g1.STNumPoints() AS G1, @g2.STNumPoints() AS G2;
 ```  
  
## <a name="see-also"></a>另請參閱  
 [STLength &#40; geography 資料類型 &#41;](../../t-sql/spatial-geography/stlength-geography-data-type.md)   
 [STNumPoints &#40; geography 資料類型 &#41;](../../t-sql/spatial-geography/stnumpoints-geography-data-type.md)   
 [空間資料類型概觀](../../relational-databases/spatial/spatial-data-types-overview.md)  
  
  

