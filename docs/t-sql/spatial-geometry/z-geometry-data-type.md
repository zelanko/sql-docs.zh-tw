---
description: Z (geometry 資料類型)
title: Z (geometry 資料類型) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- Z (geometry Data Type)
- Z_(geometry_Data_Type)_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Z (geometry Data Type)
ms.assetid: a62ed736-44df-4591-9109-ce90e1df9bd3
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 2e90df19c6d6946c17b554c9195c03bce3f55ca8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88472368"
---
# <a name="z-geometry-data-type"></a>Z (geometry 資料類型)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

例項的 Z (高度) 值。 高度值的語意為使用者所定義。
  
## <a name="syntax"></a>語法  
  
```  
  
.Z  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>傳回型別
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 類型：**float**  
  
 CLR 類型：**SqlDouble**  
  
## <a name="remarks"></a>備註  
 除了對於未設定此屬性的任何 **Point** 執行個體而言，此屬性的值會是 Null 之外，如果 geometry 執行個體不是點，此屬性也會是 Null。  
  
 這個屬性是唯讀的。  
  
 Z 座標不會用於程式庫所做的任何計算，也不會透過任何程式庫計算來夾帶。  
  
## <a name="examples"></a>範例  
 下列範例會建立具有 Z (高度) 和 M (測量) 值的 `Point` 例項，並使用 `Z` 提取此例項的 Z 值。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POINT(1 2 3 4)', 0);  
SELECT @g.Z;  
```  
  
## <a name="see-also"></a>另請參閱  
 [M &#40;geometry 資料類型&#41;](../../t-sql/spatial-geometry/m-geometry-data-type.md)   
 [AsTextZM &#40;geometry 資料類型&#41;](../../t-sql/spatial-geometry/astextzm-geometry-data-type.md)   
 [幾何例項上擴充的方法](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
  
  

