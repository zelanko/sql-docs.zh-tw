---
title: STSrid (geography 資料型別) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STSrid (geography Data Type)
- STSrid_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STSrid method
ms.assetid: 6b04f5a7-2e69-4d34-901e-b61ba6ca9c14
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: 96a8577d621b9cc8b22e0f3b334b1d9831fdcad7
ms.sourcegitcommit: 57c3b07cba5855fc7b4195a0586b42f8b45c08c2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/20/2019
ms.locfileid: "65939160"
---
# <a name="stsrid-geography-data-type"></a>STSrid (geography 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  **STSrid** 是一個整數，其代表此執行個體的空間參考識別碼 (SRID)。  
  
## <a name="syntax"></a>語法  
  
```  
  
.STSrid  
```  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 型別：**int**  
  
 CLR 類型：**SqlInt32**  
  
## <a name="remarks"></a>Remarks  
 這個屬性可以修改。  
  
## <a name="examples"></a>範例  
 第一個範例會建立一個具有 SRID 值 4326 (WGS84) 的 `geography` 例項，並使用 `STSrid` 來確認此 SRID。  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STSrid;  
```  
  
 第二個範例會使用 `STSrid` 將此例項的 SRID 值變更為 4267 (NAD27)，然後確認修改過的 SRID 值。  
  
```  
SET @g.STSrid = 4267;  
SELECT @g.STSrid;  
```  
  
## <a name="see-also"></a>另請參閱  
 [地理執行個體上的 OGC 方法](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)   
 [空間參考識別碼 &#40;SRIDs&#41;](../../relational-databases/spatial/spatial-reference-identifiers-srids.md)  
  
  
