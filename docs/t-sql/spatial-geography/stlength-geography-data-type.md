---
title: STLength (geography 資料類型) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|spatial-geography
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- STLength (geography Data Type)
- STLength_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STLength method
ms.assetid: 774560ab-4a4a-4058-b043-1e67cf6fb9eb
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2aad66648658b34b08e798aa8d3d206674cdffb4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="stlength-geography-data-type"></a>STLength (geography 資料類型)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  傳回 **GeometryCollection** 中 **geography** 執行個體或 **geography** 執行個體內的元素總長度。  
  
## <a name="syntax"></a>語法  
  
```  
  
.STLength ( )  
```  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**float**  
  
 CLR 傳回類型：**SqlDouble**  
  
## <a name="remarks"></a>Remarks  
 如果 **geography** 執行個體為封閉式的，它的長度會計算為此執行個體周圍的總長度；任何多邊形的長度就是它的周長，而且點的長度為 0。 **GeometryCollection** 長度的計算方式是加總集合所包含之所有 **geography** 執行個體的長度。  
  
 STLength() 可在有效與無效的 LineString 上運作。 一般而言，LineString 無效的原因是重疊的線段，而這可能是由不正確的 GPS 追蹤等異常所造成。 STLength() 不會移除重疊或無效的線段。 它會在所傳回的長度值中包含重疊和無效的線段。 MakeValid() 方法可以從 LineString 中移除重疊的線段。  
  
## <a name="examples"></a>範例  
 下列範例會建立 `LineString` 執行個體，並使用 `STLength()` 來尋找此執行個體的長度。  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STLength();  
```  
  
## <a name="see-also"></a>另請參閱  
 [地理例項上的 OGC 方法](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
