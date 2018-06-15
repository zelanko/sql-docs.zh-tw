---
title: Parse (geography 資料型別) | Microsoft Docs
ms.custom: ''
ms.date: 07/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|spatial-geography
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- Parse method
- Parse (geography Data Type)
ms.assetid: 21c402fa-fd0f-4d09-a097-49cee0316d4e
caps.latest.revision: 18
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 0a5e8fad6f0980d8ca8c03059b6828d2a6366639
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "33059485"
---
# <a name="parse-geography-data-type"></a>Parse (geography 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

從開放地理空間協會 (OGC) 已知的文字 (WKT) 表示法傳回 **geography** 執行個體。 Parse() 相當於 [STGeomFromText](../../t-sql/spatial-geography/stgeomfromtext-geography-data-type.md)，但是例外之處是它會採用空間參考識別碼 (SRID) 4326 當做參數。 輸入可能會夾帶選擇性 Z (高度) 和 M (測量) 值。
  
這個 **geography** 資料類型方法可支援 **FullGlobe** 執行個體或大於半球的空間執行個體。
  
## <a name="syntax"></a>語法  
  
```  
  
Parse ( 'geography_tagged_text' )  
```  
  
## <a name="arguments"></a>引數  
 *geography_tagged_text*  
 傳回之 **geography** 執行個體的 WKT 表示法。 *geography_tagged_text* 是一個 **nvarchar** 運算式。  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**geography**  
  
 CLR 傳回類型：**SqlGeography**  
  
## <a name="remarks"></a>Remarks  
 `Parse()` 傳回之 **geography** 執行個體的 OGC 型別會設定為對應的 WKT 輸入。  
  
 'Null' 字串將會解譯為 null **geography** 執行個體。  
  
 如果輸入包含對蹠邊緣，這個方法會擲回 **ArgumentException**。  
  
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
  
  
