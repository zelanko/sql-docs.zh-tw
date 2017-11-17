---
title: "STLineFromWKB (geography 資料類型) |Microsoft 文件"
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
f1_keywords:
- STLineFromWKB (geography Data Type)
- STLineFromWKB_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STLineFromWKB method
ms.assetid: 8ac2b772-6673-4ba1-a7ab-3b4b5841560b
caps.latest.revision: 15
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2aae934d52c2432f8815c278950138fc644dfd5d
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="stlinefromwkb-geography-data-type"></a>STLineFromWKB (geography 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

傳回**geography<**從開放式地理空間協會 (OGC) 已知二進位 (well-known binary，WKB) 表示法的執行個體。
  
## <a name="syntax"></a>語法  
  
```  
  
STLineFromWKB ( 'WKB_linestring' , SRID )  
```  
  
## <a name="arguments"></a>引數  
 *WKB_linestring*  
 是的 WKB 表示法**geography<**您想要傳回的執行個體。 *WKB_linestring*是**varbinary （max)**運算式。  
  
 *SRID*  
 是**int**運算式，表示的空間參考識別碼 (SRID) 的**geography<**您想要傳回的執行個體。  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回型別：**地理位置**  
  
 CLR 傳回類型： **SqlGeography**  
  
 OGC 類型： **LineString**  
  
## <a name="remarks"></a>備註  
 這個方法會擲回**FormatException**如果輸入格式不正確。  
  
## <a name="examples"></a>範例  
 下列範例會使用`STLineFromWKB()`建立`geography`執行個體。  
  
```  
DECLARE @g geography;  
SET @g = geography::STLineFromWKB(0x010200000002000000D7A3703D0A975EC08716D9CEF7D34740CBA145B6F3955EC08716D9CEF7D34740, 4326);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>另請參閱  
 [OGC 靜態地理方法](../../t-sql/spatial-geography/ogc-static-geography-methods.md)  
  
  

