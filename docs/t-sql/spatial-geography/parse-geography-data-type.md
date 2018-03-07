---
title: "剖析 (geography 資料類型) |Microsoft 文件"
ms.custom: 
ms.date: 07/30/2017
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
- Parse method
- Parse (geography Data Type)
ms.assetid: 21c402fa-fd0f-4d09-a097-49cee0316d4e
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c29c43af7034f86fa993fc5f12046200216ec57f
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="parse-geography-data-type"></a>Parse (geography 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

傳回**geography**從開放式地理空間協會 (OGC) 已知文字 (well-known text，WKT) 表示法的執行個體。 Parse() 相當於[STGeomFromText](../../t-sql/spatial-geography/stgeomfromtext-geography-data-type.md)，只不過它會採用空間參考識別碼 (SRID) 4326 當做參數。 輸入可能會夾帶選擇性 Z (高度) 和 M (測量) 值。
  
這**geography**資料類型方法可支援**FullGlobe**執行個體或大於半球的空間執行個體。
  
## <a name="syntax"></a>語法  
  
```  
  
Parse ( 'geography_tagged_text' )  
```  
  
## <a name="arguments"></a>引數  
 *geography_tagged_text*  
 是的 WKT 表示法**geography**来傳回執行個體。 *geography_tagged_text*是**nvarchar**運算式。  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回型別：**地理位置**  
  
 CLR 傳回類型： **SqlGeography**  
  
## <a name="remarks"></a>備註  
 OGC 類型**geography**所傳回的執行個體`Parse()`設定為對應的 WKT 輸入。  
  
 'Null' 將被解譯為 null 值的字串**geography**執行個體。  
  
 這個方法會擲回**ArgumentException**如果輸入包含對蹠邊緣。  
  
## <a name="examples"></a>範例  
 下列範例會使用 `Parse()` 建立 `geography` 例項。  
  
```  
DECLARE @g geography;   
SET @g = geography::Parse('LINESTRING(-122.360 47.656, -122.343 47.656)');  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>另請參閱  
 [擴充的靜態地理方法](../../t-sql/spatial-geography/extended-static-geography-methods.md)   
 [STGeomFromText &#40;geography 資料類型&#41;](../../t-sql/spatial-geography/stgeomfromtext-geography-data-type.md)  
  
  
