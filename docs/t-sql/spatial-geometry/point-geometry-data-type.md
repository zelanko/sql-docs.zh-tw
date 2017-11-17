---
title: "點 (geometry 資料類型) |Microsoft 文件"
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- Point
- Point_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Point (geometry Data Type)
ms.assetid: 7a2e593a-4d4c-4214-b0c5-02d1ac46bc66
caps.latest.revision: 15
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e153b3bbaf18e6c4b69171e56f2fdae6965396a7
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="point-geometry-data-type"></a>Point (geometry 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

建構**幾何**執行個體，代表**點**來自其 X 和 Y 值與 SRID 的執行個體。
  
## <a name="syntax"></a>語法  
  
```  
  
Point ( X, Y, SRID )  
```  
  
## <a name="arguments"></a>引數  
 *X*  
 是**float**運算式表示的 X 座標**點**產生。  
  
 *Y*  
 是**float**運算式表示的 Y 座標**點**產生。  
  
 *SRID*  
 是**int**運算式，表示的空間參考識別碼 (SRID) 的**幾何**您想要傳回的執行個體。  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回型別：**幾何**  
  
 CLR 傳回類型： **SqlGeometry**  
  
## <a name="remarks"></a>備註  
  
## <a name="examples"></a>範例  
 下列範例會使用 `Point()` 建立 `geometry` 例項。  
  
```  
DECLARE @g geometry;   
SET @g = geometry::Point(1, 10, 0);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>另請參閱  
 [擴充的靜態幾何方法](../../t-sql/spatial-geometry/extended-static-geometry-methods.md)  
  
  


