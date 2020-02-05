---
title: MultiPoint | Microsoft Docs
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- MultiPoint geometry subtype [SQL Server]
ms.assetid: 2aaab211-3aba-4dbd-90b7-095d997b1f62
author: MladjoA
ms.author: mlandzic
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 0b045ca8fd9d93ab2c088d898bd86fafe7acfc60
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "68048636"
---
# <a name="multipoint"></a>MultiPoint
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  **MultiPoint** 是零或多個點的集合。 **MultiPoint** 執行個體的界限是空的。  
  
## <a name="examples"></a>範例  

### <a name="example-a"></a>範例 A。
下列範例會建立具有 SRID 23 和兩個點的 `geometry MultiPoint` 執行個體：一個點的座標為 (2, 3)，另一個點的座標為 (7, 8)，而 Z 值為 9.5。  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('MULTIPOINT((2 3), (7 8 9.5))', 23);  
```  
  
### <a name="example-b"></a>範例 B. 
下列範例使用 `MultiPoint` 來表示 `STMPointFromText()` 執行個體。  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::STMPointFromText('MULTIPOINT((2 3), (7 8 9.5))', 23);  
```  
  
### <a name="example-c"></a>範例 C。
下列範例使用 `STGeometryN()` 方法來擷取集合中第一個點的描述。  
  
```sql  
SELECT @g.STGeometryN(1).STAsText();  
```  
  
## <a name="see-also"></a>另請參閱  
 [點](../../relational-databases/spatial/point.md)   
 [空間資料 &#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md)  
  
  
