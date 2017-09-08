---
title: "IsValidDetailed (geography 資料類型) |Microsoft 文件"
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
- IsValidDetailed_TSQL
- IsValidDetailed
dev_langs:
- TSQL
helpviewer_keywords:
- IsValidDetailed geography
ms.assetid: f5f0b753-c825-43ce-987d-98655d8d8702
caps.latest.revision: 8
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: abe552b7afda98443decf0b66e81ae74f8a32b00
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="isvaliddetailed-geography-data-type"></a>IsValidDetailed (geography 資料類型)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

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
DECLARE @p GEOGRAPHY = 'Polygon((2 2, 4 4, 4 2, 2 4, 2 2))'  
SELECT @p.IsValidDetailed()  
--Returns: 24409: Not valid because some portion of polygon ring (1) lies in the interior of a polygon.  
```  
  
## <a name="see-also"></a>另請參閱  
 [Geography 執行個體上的擴充的方法](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
