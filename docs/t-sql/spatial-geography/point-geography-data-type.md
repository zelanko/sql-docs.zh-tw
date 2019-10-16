---
title: Point (geography 資料型別) | Microsoft Docs
ms.custom: ''
ms.date: 10/10/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 665497328238fbaa88d666fb214af336531e93c7
ms.sourcegitcommit: aece9f7db367098fcc0c508209ba243e05547fe1
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/11/2019
ms.locfileid: "72260166"
---
# <a name="point-geography-data-type"></a>Point (geography 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

建構 **geography** 執行個體，這個執行個體會根據其緯度和經度值與空間參考識別碼 (SRID) 來表示 **Point** 執行個體。
  
## <a name="syntax"></a>語法  
  
```  
  
Point ( Lat, Long, SRID )  
```  
  
## <a name="arguments"></a>引數  
 *Lat*  
 這是 **float** 運算式，代表所要產生之 **Point** 的 X 座標。  
  
 *Long*  
 這是 **float** 運算式，代表所要產生之 **Point** 的 Y 座標。 如需有關有效緯度和經度值的詳細資訊，請參閱 [Point](../../relational-databases/spatial/point.md)。  
  
 *SRID*  
 這是 **int** 運算式，代表要傳回之**地理**執行個體的[空間參考識別碼](https://docs.microsoft.com/sql/relational-databases/spatial/spatial-reference-identifiers-srids)。  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**geography**  
  
 CLR 傳回型別：**SqlGeography**  
  
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
  
  
