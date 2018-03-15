---
title: "STNumPoints (geometry 資料型別) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
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
- STNumPoints_TSQL
- STNumPoints (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STNumPoints (geometry Data Type)
ms.assetid: a19520fc-7f91-4a2c-856f-4d8b99a7e496
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 51e08f456377ecef45bd26fc53a7a546c95220fb
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
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
  
 CLR 傳回類型：**SqlInt32**  
  
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
  
  
