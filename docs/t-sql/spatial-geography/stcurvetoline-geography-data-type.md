---
title: "STCurveToLine (geography 資料類型) |Microsoft 文件"
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
- STCurveToLine_TSQL
- STCurveToLine
dev_langs: TSQL
helpviewer_keywords: STCurveToLine method (geography)
ms.assetid: 2f863a85-6168-465a-b32f-bb5e3de58dee
caps.latest.revision: "12"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d8353ac3184c6c51668c0da9bce5ab9d33c19b5b
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/19/2018
---
# <a name="stcurvetoline-geography-data-type"></a>STCurveToLine (geography 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

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
  
  
