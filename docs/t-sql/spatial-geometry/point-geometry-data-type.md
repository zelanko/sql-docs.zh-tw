---
title: Point (geometry 資料類型) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
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
- Point (geometry Data Type)
ms.assetid: 7a2e593a-4d4c-4214-b0c5-02d1ac46bc66
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: da858d3f778a6e1177975107418f6640d68d086b
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85748843"
---
# <a name="point-geometry-data-type"></a>Point (geometry 資料類型)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

從 **Point** 執行個體的 X 和 Y 值及 SRID 來建構代表它的 **geometry** 執行個體。
  
## <a name="syntax"></a>語法  
  
```  
  
Point ( X, Y, SRID )  
```  
  
## <a name="arguments"></a>引數  
 *X*  
 這是 **float** 運算式，代表所要產生之 **Point** 的 X 座標。  
  
 *Y*  
 這是 **float** 運算式，代表所要產生之 **Point** 的 Y 座標。  
  
 *SRID*  
 這是 **int** 運算式，代表要傳回之 **geometry** 執行個體的空間參考識別碼 (SRID)。  
  
## <a name="return-types"></a>傳回型別  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**geometry**  
  
 CLR 傳回類型：**SqlGeometry**  
  
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
  
  

