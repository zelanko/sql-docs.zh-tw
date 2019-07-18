---
title: STIsClosed (geography 資料類型) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STIsClosed (geography Data Type)
- STIsClosed_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STIsClosed method
ms.assetid: eba1643f-07c4-4500-8643-b7e90f908147
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: a283ce663ce8aa68418169a8cb3bbb310c3b766c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65936796"
---
# <a name="stisclosed-geography-data-type"></a>STIsClosed (geography 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  如果給定的 **geography** 執行個體的起點和終點相同，就會傳回 1。 如果每一個包含的 **geography** 執行個體都是封閉式，則會針對 **geography** 集合類型傳回 1。 如果此執行個體不是封閉式，就會傳回 0。  
  
 這個 **geography** 資料類型方法可支援 **FullGlobe** 執行個體或大於半球的空間執行個體。  
  
## <a name="syntax"></a>語法  
  
```  
  
.STIsClosed ( )  
```  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**bit**  
  
 CLR 傳回型別：**SqlBoolean**  
  
## <a name="remarks"></a>Remarks  
 如果 **geography** 執行個體的任何數據是點，或是這個執行個體是空的，則此方法會傳回 0。  
  
 如果 **FullGlobe** 執行個體是 **Polygon** 或其他類型的執行個體，則此方法會傳回 True。  
  
 所有 **Polygon** 執行個體都會被視為封閉式。  
  
## <a name="examples"></a>範例  
 下列範例會建立 `Polygon` 執行個體，並使用 `STIsClosed()` 來測試 `Polygon` 是否為封閉式。  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))', 4326);  
SELECT @g.STIsClosed();  
```  
  
## <a name="see-also"></a>另請參閱  
 [地理例項上的 OGC 方法](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
