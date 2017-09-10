---
title: "Long (geography 資料類型) |Microsoft 文件"
ms.custom: 
ms.date: 06/02/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- Long_TSQL
- Long
dev_langs:
- TSQL
helpviewer_keywords:
- Long method
ms.assetid: bedbeced-70b8-4569-84f3-f86bfb04ce50
caps.latest.revision: 14
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0c69ce921e8aa22d65011a56d47c5cd7b05ad76f
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="long-geography-data-type"></a>Long (geography 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  經度屬性**geography**執行個體。  
  
## <a name="syntax"></a>語法  
  
```  
  
.Long  
```  
  
## <a name="return-value"></a>傳回值  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]類型： **float**  
  
 CLR 型別： **SqlDouble**  
  
## <a name="remarks"></a>備註  
 在了 OpenGIS 模型中，長時間定義只有**geography**執行個體所組成的單一點。 如果這個屬性會傳回 NULL **geography**執行個體包含多個單一點。 這個屬性是精確且唯讀的。  
  
## <a name="examples"></a>範例  
 這個範例會建立**點**執行個體，並擷取點的經度。  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POINT(-122.34900 47.65100)', 4326);  
SELECT @g.Long;  
```  
  
## <a name="see-also"></a>另請參閱  
 [Geography 執行個體上的擴充的方法](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  

