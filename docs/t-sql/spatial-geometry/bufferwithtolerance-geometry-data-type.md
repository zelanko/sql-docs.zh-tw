---
title: "BufferWithTolerance (geometry 資料類型) |Microsoft 文件"
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
- BufferWithTolerance_TSQL
- BufferWithTolerance
dev_langs:
- TSQL
helpviewer_keywords:
- BufferWithTolerance (geometry Data Type)
ms.assetid: 7049d37a-3e72-4e93-87a1-c96a6f0e2b99
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1cb8520351369dad761862132211b5222c52e3ae
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="bufferwithtolerance-geometry-data-type"></a>BufferWithTolerance (geometry 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

傳回幾何物件，此物件表示聯集的所有點值從距離**幾何**執行個體小於或等於指定值，允許指定的容錯。
  
## <a name="syntax"></a>語法  
  
```  
  
.BufferWithTolerance ( distance, tolerance, relative )  
```  
  
## <a name="arguments"></a>引數  
 *distance*  
 是**float**運算式指定從距離**幾何**執行個體的周圍計算緩衝。  
  
 *tolerance*  
 是**float**運算式，指定緩衝距離的容錯。  
  
 *容錯*指的是傳回之線性近似值之理想緩衝距離的最大變異。  
  
 例如，點的理想緩衝距離是圓形，但是這必須由多邊形來模擬。 當容錯越小時，多邊形就會有越多的點，這樣會增加結果的複雜度，但是會減少錯誤。  
  
 *relative*  
 是**元**指定是否*容錯*值是相對或絕對。 如果 'TRUE' 或 1，然後容錯為相對值，而且會計算的產品為*容錯*參數及週框方塊之直徑的執行個體。 如果 'FALSE' 或 0，容錯為絕對值，*容錯*值是傳回之線性近似值之理想緩衝距離的最大絕對變異。  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回型別：**幾何**  
  
 CLR 傳回類型： **SqlGeometry**  
  
## <a name="exceptions"></a>例外狀況  
 *容錯*參數必須是大於零。 如果*容錯*< = 0 則`System.ArgumentOutOfRangeException`就會擲回。  
  
> [!NOTE]  
>  因為*容錯*是**float**型別，`System.Runtime.InteropServices.COMException`如果給定的容錯值是非常小，因為浮點類型的捨入問題可能會擲回。  
  
## <a name="remarks"></a>備註  
 當*距離*> 0，則**多邊形**或**MultiPolygon**會傳回執行個體。  
  
> [!NOTE]  
>  因為 distance 是**float**，極小的值可等同於零的計算中。 當發生這種情況，一份呼叫**幾何**會傳回執行個體。 請參閱[float 和 real &#40;TRANSACT-SQL &#41;](../../t-sql/data-types/float-and-real-transact-sql.md).  
  
 當*距離*= 0，則呼叫副本**幾何**會傳回執行個體。  
  
 當*距離*< 0 則  
  
-   空白**GeometryCollection**當執行個體的維度是 0 或 1，則會傳回執行個體。  
  
-   當執行個體的維度是 2 或以上，則傳回負數緩衝。  
  
    > [!NOTE]  
    >  負數緩衝也可能會建立空**GeometryCollection**執行個體。  
  
 負數緩衝會移除界限之給定距離內的所有點**幾何**執行個體。  
  
 理論與計算的緩衝間的錯誤是最大值 (tolerance，範圍\*1.e-7) 容限是值的其中*容錯*參數。 如需有關範圍的詳細資訊，請參閱[geometry 資料類型方法參考](http://msdn.microsoft.com/library/d88e632b-6b2f-4466-a15f-9fbef1a347a7)。  
  
## <a name="examples"></a>範例  
 下列範例會建立 `Point` 執行個體，並使用 `BufferWithTolerance()` 來取得其周圍的約略緩衝。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POINT(3 3)', 0);  
SELECT @g.BufferWithTolerance(1, .5, 0).ToString();  
```  
  
## <a name="see-also"></a>另請參閱  
 [STBuffer &#40; geometry 資料類型 &#41;](../../t-sql/spatial-geometry/stbuffer-geometry-data-type.md)   
 [幾何例項上擴充的方法](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
  
  

