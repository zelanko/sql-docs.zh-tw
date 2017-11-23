---
title: "STMPointFromText (geometry 資料類型) |Microsoft 文件"
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STMPointFromText (geometry Data Type)
- STMPointFromText_TSQL
dev_langs: TSQL
helpviewer_keywords: STMPointFromText (geometry Data Type)
ms.assetid: 37059074-5ee8-4f55-9414-1e958fd3adaf
caps.latest.revision: "21"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: baeba01d67da4e5e395d45061600068cab6fd954
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="stmpointfromtext-geometry-data-type"></a>STMPointFromText (geometry 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

傳回**幾何**執行個體所執行的執行個體夾帶任何 Z （高度） 和 M （測量） 值的開放式地理空間協會 (OGC) 已知文字 (well-known text，WKT) 表示法。
  
## <a name="syntax"></a>語法  
  
```  
  
STMPointFromText ( 'multipoint_tagged_text', SRID )  
```  
  
## <a name="arguments"></a>引數  
 *multipoint_tagged_text*  
 是的 WKT 表示法**geometryMultiPoint**您想要傳回的執行個體。 *multipoint_tagged_text*是**nvarchar （max)**運算式。  
  
 *SRID*  
 是**int**運算式，表示的空間參考識別碼 (SRID) 的**geometryMultiPoint**您想要傳回的執行個體。  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回型別：**幾何**  
  
 CLR 傳回類型： **SqlGeometry**  
  
 OGC 類型： **MultiPoint**  
  
## <a name="remarks"></a>備註  
 這個方法會擲回**FormatException**如果輸入格式不正確。  
  
## <a name="examples"></a>範例  
 下列範例會使用 `STMPointFromText()` 建立 `geometry` 例項。  
  
```  
DECLARE @g geometry;   
SET @g = geometry::STMPointFromText('MULTIPOINT ((100 100), (200 200))', 0);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>請參閱＜  
 [OGC 靜態幾何方法](../../t-sql/spatial-geometry/ogc-static-geometry-methods.md)  
  
  

