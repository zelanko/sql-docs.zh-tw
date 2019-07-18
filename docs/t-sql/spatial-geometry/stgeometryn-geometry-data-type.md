---
title: STGeometryN (geometry 資料型別) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STGeometryN_TSQL
- STGeometryN (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STGeometryN (geometry Data Type)
ms.assetid: 348c7047-3442-4590-8879-fe841e79058c
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: 7e494349d40f78d1f6886e3091c3399b3f25e55d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65938918"
---
# <a name="stgeometryn-geometry-data-type"></a>STGeometryN (geometry 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

傳回**幾何集合**中的指定幾何。
  
## <a name="syntax"></a>語法  
  
```  
  
.STGeometryN ( expression )  
```  
  
## <a name="arguments"></a>引數  
 *expression*  
 這是介於 1 和 **geometrycollection** 內的 **geometry** 執行個體數目之間的 **int** 運算式。  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**geometry**  
  
 CLR 傳回型別：**SqlGeometry**  
  
## <a name="remarks"></a>Remarks  
 如果參數大於 `STNumGeometries()` 的結果，這個方法會傳回 **null**；如果 *expression* 參數小於 1，將會擲回 **ArgumentOutOfRangeException**。  
  
## <a name="examples"></a>範例  
 下列範例會建立 `MultiPoint``geometry collection` 並使用 `STGeometryN()` 來尋找集合的第二個 `geometry` 執行個體。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('MULTIPOINT(0 0, 13.5 2, 7 19)', 0);  
SELECT @g.STGeometryN(2).ToString();  
```  
  
## <a name="see-also"></a>另請參閱  
 [幾何例項上的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

