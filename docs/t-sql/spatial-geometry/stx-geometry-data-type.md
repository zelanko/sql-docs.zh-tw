---
description: STX (geometry 資料類型)
title: STX (geometry 資料型別) | Microsoft Docs
ms.custom: ''
ms.date: 06/23/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STX (geometry Data Type)
- STX_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STX (geometry Data Type)
ms.assetid: 2aef77e8-0460-43f9-bad6-2aae6d8c36f9
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 975126e2aa7c1628493894f433e82c9d5619f52e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88472405"
---
# <a name="stx-geometry-data-type"></a>STX (geometry 資料類型)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

**Point** 執行個體的 X 座標屬性。
  
## <a name="syntax"></a>語法  
  
```  
  
.STX  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>傳回型別
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 類型：**float**  
  
 CLR 類型：**SqlDouble**  
  
## <a name="remarks"></a>備註  
 如果 **geometry** 執行個體不是點，這個屬性的值將會是 Null。  
  
 這個屬性是唯讀的。  
  
## <a name="examples"></a>範例  
 下列範例會建立 `Point` 例項，並使用 `STX` 來擷取此例項的 X 座標。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POINT(3 8)', 0);  
SELECT @g.STX;  
```  
  
## <a name="see-also"></a>另請參閱  
 [STY &#40;geometry 資料類型&#41;](../../t-sql/spatial-geometry/sty-geometry-data-type.md)   
 [STSrid &#40;geometry 資料型別&#41;](../../t-sql/spatial-geometry/stsrid-geometry-data-type.md)   
 [幾何例項上的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

