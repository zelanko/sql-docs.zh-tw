---
title: "IsValidDetailed (geometry 資料類型) |Microsoft 文件"
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords: IsValidDetailed geometry
ms.assetid: 5a31e88a-ad7b-4ef7-b773-e2571f1cb3aa
caps.latest.revision: "7"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 55b67a0a3db22697b9f320f3c8861b08e09a2475
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="isvaliddetailed-geometry-datatype"></a>IsValidDetailed (geometry 資料類型)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

傳回訊息，有助於識別空間物件無效的問題。 如果物件為無效，只會傳回第一個錯誤。 如果物件為有效，則會傳回值 24400。
  
## <a name="syntax"></a>語法  
  
```  
  
.IsValidDetailed()  
```  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回型別： **nvarchar （max)**  
  
 CLR 傳回類型：**字串**  
  
## <a name="remarks"></a>備註  
 下表包含可能的傳回值：  
  
|傳回值|Description|  
|------------------|-----------------|  
|24400|有效|  
|24401|無效，原因未知。|  
|24402|無效，因為點 {0} 是隔離點，而這在這種類型的物件中無效。|  
|24403|無效，因為有些成對的多邊形邊緣重疊。|  
|24404|無效，因為多邊環形 {0} 與其自身或其他環形交叉。|  
|24405|無效，因為有些多邊環形與其自身或其他環形交叉。|  
|24406|無效，因為曲線 {0} 變質成點。|  
|24407|無效，因為多邊環形 {0} 選取範圍摺疊點 {1} 一行。|  
|24408|無效，因為多邊環形 {0} 未封閉。|  
|24409|無效，因為多邊環形 {0} 的某些部分在多邊形內部。|  
|24410|無效，因為環形 {0} 是多邊形中的第一個環，卻不是它的外環。|  
|24411|無效，因為環形 {0} 超出其多邊形的環形 {1}。|  
|24412|無效，因為環形 {0} 與 {1} 的多邊形內部不連接在一起。|  
|24413|無效，因為曲線 {0} 中有兩個重疊的邊緣。|  
|24414|無效，因為曲線 {0} 邊緣 1 曲線 \} 的邊緣重疊。|  
|24415|無效，因為有些多邊形的環形結構無效。|  
|24416|無效，因為在曲線 {0} 點開始的邊緣 {1} 是直線或具有對蹠端點的變質弧線。|  
  
## <a name="examples"></a>範例  
 無效的空間物件的下列範例說明如何**isvaliddetailed （)**方法的行為。  
  
```tsql  
DECLARE @p GEOMETRY = 'Polygon((2 2, 4 4, 4 2, 2 4, 2 2))'  
SELECT @p.IsValidDetailed()  
--Returns: 24404: Not valid because polygon ring (1) intersects itself or some other ring.  
```  
  
## <a name="see-also"></a>請參閱＜  
 [幾何例項上擴充的方法](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
  
  

