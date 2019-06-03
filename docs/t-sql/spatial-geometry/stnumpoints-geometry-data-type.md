---
title: STNumPoints (geometry 資料型別) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STNumPoints_TSQL
- STNumPoints (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STNumPoints (geometry Data Type)
ms.assetid: a19520fc-7f91-4a2c-856f-4d8b99a7e496
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: 1eb97aa0ec64552049a33f9483beb5318a39ff48
ms.sourcegitcommit: 57c3b07cba5855fc7b4195a0586b42f8b45c08c2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/20/2019
ms.locfileid: "65938503"
---
# <a name="stnumpoints-geometry-data-type"></a>STNumPoints (geometry 資料類型)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  傳回 **geometry** 執行個體中每一個圖形內的點數總和。  
  
## <a name="syntax"></a>語法  
  
```  
  
.STNumPoints ( )  
```  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**int**  
  
 CLR 傳回型別：**SqlInt32**  
  
## <a name="remarks"></a>Remarks  
 此方法會算入 **geometry** 執行個體描述中的點。 重複的點都會被算入。 如果此執行個體為 **collection** 型別，這個方法會傳回它的每一個元素內點的總和。  
  
## <a name="examples"></a>範例  
 下列範例會建立 `LineString` 例項，並使用 `STNumPoints()` 來判斷例項描述內所用的點數。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 1 0)', 0);  
SELECT @g.STNumPoints();  
```  
  
## <a name="see-also"></a>另請參閱  
 [幾何例項上的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  
