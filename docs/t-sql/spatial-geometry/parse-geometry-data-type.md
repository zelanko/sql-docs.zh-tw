---
title: "剖析 (geometry 資料類型) |Microsoft 文件"
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
dev_langs:
- TSQL
helpviewer_keywords:
- Parse (geometry Data Type)
ms.assetid: 6e080919-4b64-46cd-8dd2-254a9c232e53
caps.latest.revision: 19
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 64adf9398a6ea63203f75714aa97ccf2653e947b
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="parse-geometry-data-type"></a>Parse (geometry 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

傳回**幾何**從開放式地理空間協會 (OGC) 已知文字 (well-known text，WKT) 表示法的執行個體。 `Parse()`相當於[Stgeomfromtext](../../t-sql/spatial-geometry/parse-geometry-data-type.md)，發生例外狀況，它會採用空間參考識別碼 (SRID) 0 當做參數。 輸入可能會夾帶選擇性 Z (高度) 和 M (測量) 值。
  
## <a name="syntax"></a>語法  
  
```  
  
Parse ( 'geometry_tagged_text' )  
```  
  
## <a name="arguments"></a>引數  
 *geometry_tagged_text*  
 是的 WKT 表示法**幾何**您想要傳回的執行個體。 *geometry_tagged_text*是**nvarchar**運算式。  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回型別：**幾何**  
  
 CLR 傳回類型： **SqlGeometry**  
  
## <a name="remarks"></a>備註  
 OGC 類型**幾何**所傳回的執行個體`Parse()`設定為對應的 WKT 輸入。  
  
 'Null' 將被解譯為 null 值的字串**幾何**執行個體。  
  
 這個方法會擲回**FormatException**如果輸入格式不正確。  
  
## <a name="examples"></a>範例  
 下列範例會使用 `Parse()` 建立 `geometry` 例項。  
  
```  
DECLARE @g geometry;   
SET @g = geometry::Parse('LINESTRING (100 100, 20 180, 180 180)');  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>另請參閱  
 [STGeomFromText](../../t-sql/spatial-geometry/parse-geometry-data-type.md)   
 [擴充的靜態幾何方法](../../t-sql/spatial-geometry/extended-static-geometry-methods.md)  
  
  


