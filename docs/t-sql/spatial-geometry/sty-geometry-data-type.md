---
title: STY (geometry 資料型別) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STY_TSQL
- STY (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STY (geometry Data Type)
ms.assetid: f72e0eaa-7d1d-4052-88fd-a172d8cb0d71
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: bf8def807299a766ab66506c4c0769705f2d0462
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85762104"
---
# <a name="sty-geometry-data-type"></a>STY (geometry 資料類型)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

**Point** 執行個體的 Y 座標屬性。
  
## <a name="syntax"></a>語法  
  
```  
  
.STY  
```  
  
## <a name="return-types"></a>傳回型別  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 類型：**float**  
  
 CLR 類型：**SqlDouble**  
  
## <a name="remarks"></a>備註  
 如果 **geometry** 執行個體是一個點，則這個屬性的值將會是 null。 這個屬性是唯讀的。  
  
## <a name="examples"></a>範例  
 下列範例會建立 `Point` 例項，並使用 `STY` 來擷取此例項的 Y 座標。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POINT(3 8)', 0);  
SELECT @g.STY;  
```  
  
## <a name="see-also"></a>另請參閱  
 [STX &#40;geometry 資料類型&#41;](../../t-sql/spatial-geometry/stx-geometry-data-type.md)   
 [STSrid &#40;geometry 資料型別&#41;](../../t-sql/spatial-geometry/stsrid-geometry-data-type.md)   
 [幾何例項上的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

