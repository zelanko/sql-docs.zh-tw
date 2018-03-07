---
title: "AsGml (geometry 資料類型) |Microsoft 文件"
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
- AsGml(geometry_Data_Type)_TSQL
- AsGml
- AsGml(geometry Data Type)
- AsGml_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- AsGml (geometry Data Type)
ms.assetid: f6c2e130-05f3-4ef3-921b-d78b51437d48
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6e95bef8ad53d9393467843fe05c67304ad4d86a
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="asgml-geometry-data-type"></a>AsGml (geometry 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

傳回的地理標記語言 (GML) 表示**幾何**執行個體。
  
如需有關地理標記語言的詳細資訊，請參閱以下開放式地理空間協會規格：[OGC 規格，地理標記語言。](http://go.microsoft.com/fwlink/?LinkId=93629)
  
## <a name="syntax"></a>語法  
  
```  
  
.AsGml ( )  
```  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回型別： **xml**  
  
 CLR 傳回類型： **SqlXml**  
  
## <a name="remarks"></a>備註  
  
## <a name="examples"></a>範例  
 下列範例會建立 `LineString` 例項，並使用 `AsGML()` 傳回此例項的 GML 描述。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 0 1, 1 0)', 0)  
SELECT @g.AsGml();  
```  
  
 這個方法會傳回 `LineString` 例項形式的描述。  
  
```  
<LineString xmlns="http://www.opengis.net/gml">  
<posList>0 0 0 1 1 0</posList></LineString>  
```  
  
## <a name="see-also"></a>另請參閱  
 [幾何例項上擴充的方法](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
  
  

