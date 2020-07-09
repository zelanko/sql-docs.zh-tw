---
title: STLength (geometry 資料類型) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STLength_TSQL
- STLength (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STLength (geometry Data Type)
ms.assetid: e34dc620-2a65-4248-b099-fff91830ab98
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 11c88132b55957a84dfc44a6cec2e6563bf23eb7
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85762365"
---
# <a name="stlength-geometry-data-type"></a>STLength (geometry 資料類型)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

傳回 **geometry** 執行個體中元素的總長度。
  
## <a name="syntax"></a>語法  
  
```  
  
.STLength ( )  
```  
  
## <a name="return-types"></a>傳回型別  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**float**  
  
 CLR 傳回類型：**SqlDouble**  
  
## <a name="remarks"></a>備註  
 如果 **geometry** 執行個體為封閉式，它的長度會計算為此執行個體周圍的總長度；任何多邊形的長度即是其周長，點的長度則為 0。 任何 **geometrycollection** 類型的長度即是其包含之 **geometry** 執行個體的長度總和。  
  
 STLength() 可在有效與無效的 LineString 上運作。 一般而言，LineString 無效的原因是重疊的線段，而這可能是由不正確的 GPS 追蹤等異常所造成。 STLength() 不會移除重疊或無效的線段。 它會在所傳回的長度值中包含重疊和無效的線段。 MakeValid() 方法可以從 LineString 中移除重疊的線段。  
  
## <a name="examples"></a>範例  
 下列範例會建立 `LineString` 執行個體，並使用 `STLength()` 來尋找此執行個體的長度。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 1 0)', 0);  
SELECT @g.STLength();  
```  
  
## <a name="see-also"></a>另請參閱  
 [幾何例項上的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

