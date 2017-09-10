---
title: "點 (geography 資料類型) |Microsoft 文件"
ms.custom: 
ms.date: 07/30/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
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
- Point method
- Point (geography Data Type)
ms.assetid: 0dc6f422-7aae-4016-b7f4-3289fa8f989c
caps.latest.revision: 17
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7cefb6e199bbd4617b1fc2f6f71d9bb3997445dc
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="point-geography-data-type"></a>Point (geography 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

建構**geography**執行個體，代表**點**來自其緯度和經度值與空間參考識別碼 (SRID) 的執行個體。
  
## <a name="syntax"></a>語法  
  
```  
  
Point ( Lat, Long, SRID )  
```  
  
## <a name="arguments"></a>引數  
 *Lat*  
 是**float**運算式表示的 x 座標**點**產生。  
  
 *長*  
 是**float**運算式表示的 y 座標**點**產生。 如需有關有效緯度和經度值的詳細資訊，請參閱[點](../../relational-databases/spatial/point.md)。  
  
 *SRID*  
 是**int**運算式，表示的 SRID **geography**您想要傳回的執行個體。  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回型別：**地理位置**  
  
 CLR 傳回類型： **SqlGeography**  
  
> [!NOTE]  
>  引數的點 (geography 資料類型) 的方法有相較於 WKT 為反轉的座標。  
  
## <a name="examples"></a>範例  
 下列範例會使用 `Point()` 建立 `geography` 例項。  
  
```  
DECLARE @g geography;   
SET @g = geography::Point(47.65100, -122.34900, 4326)  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>另請參閱  
 [擴充的靜態地理方法](../../t-sql/spatial-geography/extended-static-geography-methods.md)  
  
  

