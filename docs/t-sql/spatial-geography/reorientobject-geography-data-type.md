---
title: "ReorientObject (geography 資料類型) |Microsoft 文件"
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
- ReorientObject
- ReorientObject_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ReorientObject method (geography)
ms.assetid: e2a1a4f1-211b-4e82-abed-03fc7140a83c
caps.latest.revision: 12
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3a32dc43776511881697b972c9279d143af917c2
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="reorientobject-geography-data-type"></a>ReorientObject (geography 資料類型)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  傳回**geography**交替之內部區域與外部區域的執行個體。  
  
 這**geography**資料類型方法可支援**FullGlobe**執行個體或大於半球的空間執行個體。  
  
## <a name="syntax"></a>語法  
  
```  
  
.ReorientObject (geography)  
```  
  
## <a name="arguments"></a>引數  
 *地理位置*  
 這是另一個**geography**所在的執行個體`ReorientObject()`叫用。  
  
## <a name="return-value"></a>傳回值  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回型別：**地理位置**  
  
 CLR 傳回類型： **SqlGeography**  
  
## <a name="remarks"></a>備註  
 這個方法會變更所有的環形方向**多邊形**中**GeometryCollection**但不會移除或變更任何**點**或**Linestrings**中指定的集合。  
  
 如果**GeometryCollection**會傳遞至這個方法，集合中的每個執行個體的方向，但不是方向都會重新調整整個集合。  
  
## <a name="examples"></a>範例  
  
```  
DECLARE @R GEOGRAPHY = GEOGRAPHY::Parse('Polygon((-10 -10, -10 10, 10 10, 10 -10, -10 -10))');  
SELECT @R.ReorientObject().STAsText();  
--Result: POLYGON ((10 10, -10 10, -10 -10, 10 -10, 10 10))  
```  
  
## <a name="see-also"></a>另請參閱  
 [Geography 執行個體上的擴充的方法](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  

