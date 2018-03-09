---
title: "Z (geography 資料類型) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
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
- Z (geography Data Type)
- Z_(geography_Data_Type)_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Z method
ms.assetid: 9abc79c5-43c9-4cc2-b37f-d2ecdec7c234
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9f1f0677d96fe12f8b425b54a63ac57bedb4a155
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="z-geography-data-type"></a>Z (geography 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  例項的 Z (高度) 值。 高度值的語意為使用者所定義。  
  
## <a name="syntax"></a>語法  
  
```  
  
.Z  
```  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]類型： **float**  
  
 CLR 型別： **SqlDouble**  
  
## <a name="remarks"></a>備註  
 這個屬性的值為 null 如果**geography**執行個體不是點，以及與任何**點**未設定它的執行個體。  
  
 此屬性是唯讀的。  
  
 Z 座標不會用於程式庫所做的任何計算，也不會透過任何程式庫計算來夾帶。  
  
## <a name="examples"></a>範例  
 下列範例會建立具有 Z (高度) 和 M (測量) 值的 `Point` 例項，並使用 `Z` 提取此例項的 Z 值。  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POINT(-122.34900 47.65100 10.3 12)', 4326);  
SELECT @g.Z;  
```  
  
## <a name="see-also"></a>另請參閱  
 [Geography 執行個體上的擴充的方法](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [M &#40; geography 資料類型 &#41;](../../t-sql/spatial-geography/m-geography-data-type.md)   
 [AsTextZM &#40;geography 資料類型&#41;](../../t-sql/spatial-geography/astextzm-geography-data-type.md)  
  
  
