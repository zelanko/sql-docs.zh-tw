---
title: Long (geography 資料類型) | Microsoft Docs
ms.custom: ''
ms.date: 06/02/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- Long_TSQL
- Long
dev_langs:
- TSQL
helpviewer_keywords:
- Long method
ms.assetid: bedbeced-70b8-4569-84f3-f86bfb04ce50
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 20f1521091a295d1293c9f3e06958f36930ba4e9
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "67930206"
---
# <a name="long-geography-data-type"></a>Long (geography 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  **geography** 執行個體的經度屬性。  
  
## <a name="syntax"></a>語法  
  
```  
  
.Long  
```  
  
## <a name="return-value"></a>傳回值  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 類型：**float**  
  
 CLR 類型：**SqlDouble**  
  
## <a name="remarks"></a>備註  
 在 OpenGIS 模型中，Long 只會在由單一點組成的 **geography** 執行個體上定義。 如果 **geography** 執行個體包含多個單一點，此屬性將會傳回 NULL。 這個屬性是精確且唯讀的。  
  
## <a name="examples"></a>範例  
 此範例會建立 **Point** 執行個體，並擷取此點的經度。  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POINT(-122.34900 47.65100)', 4326);  
SELECT @g.Long;  
```  
  
## <a name="see-also"></a>另請參閱  
 [地理例項上擴充的方法](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
