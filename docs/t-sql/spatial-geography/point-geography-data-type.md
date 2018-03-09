---
title: "點 (geography 資料類型) |Microsoft 文件"
ms.custom: 
ms.date: 07/30/2017
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
- Point method
- Point (geography Data Type)
ms.assetid: 0dc6f422-7aae-4016-b7f4-3289fa8f989c
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: f37072d64159d5d8bfb1d44a64dd017adf0fceed
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="point-geography-data-type"></a>Point (geography 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

建構**geography**執行個體，代表**點**來自其緯度和經度值與空間參考識別碼 (SRID) 的執行個體。
  
## <a name="syntax"></a>語法  
  
```  
  
Point ( Lat, Long, SRID )  
```  
  
## <a name="arguments"></a>引數  
 *Lat*  
 是**float**運算式表示的 x 座標**點**產生。  
  
 *長整數*  
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
  
  
