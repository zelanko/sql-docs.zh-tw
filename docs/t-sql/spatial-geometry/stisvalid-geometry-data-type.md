---
title: "STIsValid (geometry 資料類型) | Microsoft Docs"
ms.custom: 
ms.date: 08/03/2017
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
- STIsValid (geometry Data Type)
- STIsValid_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STIsValid (geometry Data Type)
ms.assetid: 6da39bea-0f67-4660-98fc-d7214f9b2138
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 436cab211eceff9eb286b4e44e90aa3f64b9d03c
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="stisvalid-geometry-data-type"></a>STIsValid (geometry 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

如果 **geometry** 執行個體的格式正確 (根據它的開放地理空間協會 (OGC) 類型)，就會傳回 True。 如果 **geometry** 執行個體的格式不正確，就會傳回 False。
  
## <a name="syntax"></a>語法  
  
```  
  
.STIsValid ( )  
```  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**bit**  
  
 CLR 傳回類型：**SqlBoolean**  
  
## <a name="remarks"></a>Remarks  
 可以叫用 [STGeometryType()](../../t-sql/spatial-geometry/stgeometrytype-geometry-data-type.md) 來判斷 **geometry** 執行個體的 OGC 類型。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 只會產生有效的 **geometry** 執行個體，但是允許儲存和擷取無效的執行個體。 可以使用 `MakeValid()` 方法來擷取表示任何無效例項之相同點組的有效例項。  
  
## <a name="examples"></a>範例  
 下列範例會建立 `geometry` 例項，並使用 `STIsValid()` 來測試此例項是否有效。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 1 0)', 0);  
SELECT @g.STIsValid();  
```  
  
## <a name="see-also"></a>另請參閱  
 [STGeometryType &#40;Geometry 資料類型&#41;](../../t-sql/spatial-geometry/stgeometrytype-geometry-data-type.md)   
 [MakeValid &#40;geometry 資料類型&#41;](../../t-sql/spatial-geometry/makevalid-geometry-data-type.md)   
 [幾何例項上的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

