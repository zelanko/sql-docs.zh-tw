---
title: STIsClosed (geometry 資料型別) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STIsClosed_TSQL
- STIsClosed (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STIsClosed (geometry Data Type)
ms.assetid: 14edbb22-df7b-4b8a-b16c-ac477a5d32c1
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: 1212beb7f65789ec986c45af1d1a2b2c3eb8d83f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65938829"
---
# <a name="stisclosed-geometry-data-type"></a>STIsClosed (geometry 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

如果給定的 **geometry** 執行個體的起點和終點是相同的，就會傳回 1。 如果每一個包含的 **geometry** 執行個體都是封閉式，則會針對 **geometrycollection** 型別傳回 1。 如果此執行個體不是封閉式，就會傳回 0。
  
## <a name="syntax"></a>語法  
  
```  
  
.STIsClosed ( )  
```  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**bit**  
  
 CLR 傳回型別：**SqlBoolean**  
  
## <a name="remarks"></a>Remarks  
 如果 **geometry** 執行個體的任何數據是點，或是這個執行個體是空的，則這個方法會傳回 0。  
  
 所有 **Polygon** 執行個體都會被視為封閉式。  
  
## <a name="examples"></a>範例  
 下列範例會建立 `LineString` 執行個體，並使用 `STIsClosed()` 來測試 `LineString` 是否為封閉式。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 1 0)', 0);  
SELECT @g.STIsClosed();  
```  
  
## <a name="see-also"></a>另請參閱  
 [幾何例項上的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

