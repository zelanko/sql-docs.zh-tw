---
title: "M (geometry 資料型別) | Microsoft Docs"
ms.custom: 
ms.date: 08/03/2017
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
- M (geometry Data Type)
- M_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- M (geometry Data Type)
ms.assetid: 443ae2ea-739b-41ef-96cc-ac5dfd65e10b
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 39f6677b10632363f91c2572c4a0856a67e436c3
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="m-geometry-data-type"></a>M (geometry 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  **geometry** 執行個體的 **M** (測量) 值。 measure 值的語意為使用者所定義。  

## <a name="syntax"></a>語法  
  
```  
  
.M  
```  
  
## <a name="arguments"></a>引數  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 類型：**float**  
  
 CLR 類型：**SqlDouble**  
  
## <a name="remarks"></a>Remarks  
 如果 **geometry** 執行個體不是 **Point** 以及對於未設定它的任何 **Point** 執行個體而言，這個屬性的值將會是 Null。  
  
 此屬性是唯讀的。  
  
 **M** 值不會用於程式庫所做的任何計算，也不會透過任何程式庫計算來夾帶。  
  
## <a name="examples"></a>範例  
 下列範例會建立具有 Z (高度) 和 M (測量) 值的 `Point` 例項，並使用 `M` 提取此例項的 M 值。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POINT(1 2 3 4)', 0);  
SELECT @g.M;  
```  
  
## <a name="see-also"></a>另請參閱  
 [幾何執行個體上擴充的方法](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)   
 [Z &#40;geometry 資料類型&#41;](../../t-sql/spatial-geometry/z-geometry-data-type.md)   
 [AsTextZM &#40;geometry 資料類型&#41;](../../t-sql/spatial-geometry/astextzm-geometry-data-type.md)  
  
  

