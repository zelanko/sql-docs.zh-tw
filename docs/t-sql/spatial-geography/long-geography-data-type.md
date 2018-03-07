---
title: "Long (geography 資料類型) |Microsoft 文件"
ms.custom: 
ms.date: 06/02/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- Long_TSQL
- Long
dev_langs:
- TSQL
helpviewer_keywords:
- Long method
ms.assetid: bedbeced-70b8-4569-84f3-f86bfb04ce50
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5993c081a4366338981f7bf6f86c577a8e8a189e
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="long-geography-data-type"></a>Long (geography 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  經度屬性**geography**執行個體。  
  
## <a name="syntax"></a>語法  
  
```  
  
.Long  
```  
  
## <a name="return-value"></a>傳回值  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]類型： **float**  
  
 CLR 型別： **SqlDouble**  
  
## <a name="remarks"></a>備註  
 在了 OpenGIS 模型中，長時間定義只有**geography**執行個體所組成的單一點。 如果這個屬性會傳回 NULL **geography**執行個體包含多個單一點。 這個屬性是精確且唯讀的。  
  
## <a name="examples"></a>範例  
 這個範例會建立**點**執行個體，並擷取點的經度。  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POINT(-122.34900 47.65100)', 4326);  
SELECT @g.Long;  
```  
  
## <a name="see-also"></a>另請參閱  
 [地理例項上擴充的方法](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
