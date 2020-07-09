---
title: STDisjoint (geometry 資料類型) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STDisjoint_TSQL
- STDisjoint (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STDisjoint (geometry Data Type)
ms.assetid: 90acdb21-e826-4d81-afe8-45a71f33282a
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 918445176065566676268978280929dc5bba3456
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85748667"
---
# <a name="stdisjoint-geometry-data-type"></a>STDisjoint (geometry 資料類型)
[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

  如果 **geometry** 執行個體在空間上與另一個 **geometry** 執行個體不相鄰，便傳回 1。 如果不是則傳回 0。  
  
## <a name="syntax"></a>語法  
  
```  
  
.STDisjoint ( other_geometry )  
```  
  
## <a name="arguments"></a>引數  
 *other_geometry*  
 這是要與叫用 `STDisjoint()` 所在之執行個體相比較的另一個 **geometry** 執行個體。  
  
## <a name="return-types"></a>傳回型別  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**bit**  
  
 CLR 傳回類型：**SqlBoolean**  
  
## <a name="remarks"></a>備註  
 如果兩個 **geometry** 執行個體的點組交集是空的，即表示這兩個執行個體不相鄰。  
  
 如果 **geometry** 執行個體的空間參考識別碼 (SRID) 不相符，這個方法一律會傳回 Null。  
  
## <a name="examples"></a>範例  
 下列範例會使用 `STDisjoint()` 來測試兩個 **geometry** 執行個體在空間上是否不相鄰。  
  
```  
DECLARE @g geometry;  
DECLARE @h geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 2, 2 0, 4 2)', 0);  
SET @h = geometry::STGeomFromText('POINT(1 1)', 0);  
SELECT @g.STDisjoint(@h);  
```  
  
## <a name="see-also"></a>另請參閱  
 [幾何例項上的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  
