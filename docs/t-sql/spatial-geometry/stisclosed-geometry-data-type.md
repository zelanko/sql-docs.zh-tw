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
ms.openlocfilehash: 46ed6c4f4d01b6c4ce1851c24a678617967560a7
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "67950056"
---
# <a name="stisclosed-geometry-data-type"></a>STIsClosed (geometry 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

如果給定的 **geometry** 執行個體的起點和終點是相同的，就會傳回 1。 如果每一個包含的 **geometry** 執行個體都是封閉式，則會針對 **geometrycollection** 型別傳回 1。 如果此執行個體不是封閉式，就會傳回 0。
  
## <a name="syntax"></a>語法  
  
```  
  
.STIsClosed ( )  
```  
  
## <a name="return-types"></a>傳回型別  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**bit**  
  
 CLR 傳回類型：**SqlBoolean**  
  
## <a name="remarks"></a>備註  
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
  
  

