---
title: "ShortestLineTo (geometry 資料類型) |Microsoft 文件"
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- ShortestLineTo method (geometry)
ms.assetid: 39a2d0e4-4f93-4e94-a27e-6ad9537cfe74
caps.latest.revision: 14
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: bc8843ceefe8819d2f314d76b019720863866ed1
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="shortestlineto-geometry-data-type"></a>ShortestLineTo (geometry 資料類型)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

傳回**LineString**的執行個體與兩個點代表兩者之間的最短距離**幾何**執行個體。 長度**LineString**傳回執行個體是兩者之間的距離**幾何**執行個體。
  
## <a name="syntax"></a>語法  
  
```  
  
.ShortestLineTo ( geometry_other )  
```  
  
## <a name="arguments"></a>引數  
 *geometry_other*  
 第二個**幾何**執行個體呼叫**幾何**執行個體嘗試判斷短距離。  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回型別：**幾何**  
  
 CLR 傳回類型： **SqlGeometry**  
  
## <a name="remarks"></a>備註  
 方法會傳回**LineString**與端點上框線的兩個非交集的執行個體**幾何**所比較的執行個體。 長度**LineString**傳回的等於兩個之間的最短距離**幾何**執行個體。 空白**LineString**執行個體時，會傳回兩個**幾何**執行個體彼此交集。  
  
## <a name="examples"></a>範例  
  
### <a name="a-calling-shortestlineto-on-non-intersecting-instances"></a>A. 在非交集的執行個體上呼叫 ShortestLineTo()  
 這個範例會求得 `CircularString` 執行個體和 `LineString` 執行個體之間的最短距離，並傳回連接兩點的 `LineString` 執行個體：  
  
```
 DECLARE @g1 geometry = 'CIRCULARSTRING(0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0)';  
 DECLARE @g2 geometry = 'LINESTRING(-4 7, 7 10, 3 7)';  
 SELECT @g1.ShortestLineTo(@g2).ToString();
 ```  
  
### <a name="b-calling-shortestlineto-on-intersecting-instances"></a>B. 在交集的執行個體上呼叫 ShortestLineTo()  
 本範例會傳回空白 `LineString` 執行個體，因為 `LineString` 執行個體與 `CircularString` 執行個體交集：  
  
```
 DECLARE @g1 geometry = 'CIRCULARSTRING(0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0)';  
 DECLARE @g2 geometry = 'LINESTRING(0 5, 7 10, 3 7)';  
 SELECT @g1.ShortestLineTo(@g2).ToString();
 ```  
  
## <a name="see-also"></a>另請參閱  
 [ShortestLineTo &#40; geography 資料類型 &#41;](../../t-sql/spatial-geography/shortestlineto-geography-data-type.md)  
  
  


