---
title: IsValidDetailed (geometry 資料類型) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|spatial-geography
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- IsValidDetailed geometry
ms.assetid: 5a31e88a-ad7b-4ef7-b773-e2571f1cb3aa
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 484b47de33df0f278c082831130bad233a501cf4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "33064855"
---
# <a name="isvaliddetailed-geometry-datatype"></a>IsValidDetailed (geometry 資料類型)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

傳回訊息，有助於識別空間物件無效的問題。 如果物件為無效，只會傳回第一個錯誤。 如果物件為有效，則會傳回值 24400。
  
## <a name="syntax"></a>語法  
  
```  
  
.IsValidDetailed()  
```  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**nvarchar(max)**  
  
 CLR 傳回類型：**string**  
  
## <a name="remarks"></a>Remarks  
 下表包含可能的傳回值：  
  
|傳回值|描述|  
|------------------|-----------------|  
|24400|有效|  
|24401|無效，原因未知。|  
|24402|無效，因為點 {0} 是隔離點，而這在這種類型的物件中無效。|  
|24403|無效，因為有些成對的多邊形邊緣重疊。|  
|24404|無效，因為多邊環形 {0} 與其自身或其他環形交叉。|  
|24405|無效，因為有些多邊環形與其自身或其他環形交叉。|  
|24406|無效，因為曲線 {0} 變質成點。|  
|24407|無效，因為多邊環形 {0} 在點 {1} 收合成直線。|  
|24408|無效，因為多邊環形 {0} 未封閉。|  
|24409|無效，因為多邊環形 {0} 的某些部分在多邊形內部。|  
|24410|無效，因為環形 {0} 是多邊形中的第一個環，卻不是它的外環。|  
|24411|無效，因為環形 {0} 在其多邊形的外環 {1} 外側。|  
|24412|無效，因為包含環形 {0} 和 {1} 的多邊形內部不連接。|  
|24413|無效，因為曲線 {0} 中有兩個重疊的邊緣。|  
|24414|無效，因為曲線 {0} 的邊緣與曲線 {1} 的邊緣重疊。|  
|24415|無效，因為有些多邊形的環形結構無效。|  
|24416|無效，因為在曲線 {0} 中，由點 {1} 開始的邊緣是直線或具有對蹠端點的變質弧線。|  
  
## <a name="examples"></a>範例  
 下列無效空間物件的範例說明 **IsValidDetailed()** 方法的行為。  
  
```sql  
DECLARE @p GEOMETRY = 'Polygon((2 2, 4 4, 4 2, 2 4, 2 2))'  
SELECT @p.IsValidDetailed()  
--Returns: 24404: Not valid because polygon ring (1) intersects itself or some other ring.  
```  
  
## <a name="see-also"></a>另請參閱  
 [幾何例項上擴充的方法](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
  
  

