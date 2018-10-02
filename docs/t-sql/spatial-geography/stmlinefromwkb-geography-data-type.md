---
title: STMLineFromWKB (geography 資料型別) | Microsoft Docs
ms.custom: ''
ms.date: 07/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STMLineFromWKB_TSQL
- STMLineFromWKB (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STMLineFromWKB method
ms.assetid: 05ca6d65-4799-4b9a-9672-cfebae95f23e
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 723e8f173b36b3b62cf7eece71940affc780da9d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47804849"
---
# <a name="stmlinefromwkb-geography-data-type"></a>STMLineFromWKB (geography 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

從開放地理空間協會 (OGC) 已知的二進位 (WKB) 表示法傳回 **geographyMultiLineString** 執行個體。
  
## <a name="syntax"></a>語法  
  
```  
  
STMLineFromWKB ( 'WKB_multilinestring' , SRID )  
```  
  
## <a name="arguments"></a>引數  
 *WKB_multilinestring*  
 這是您想要傳回之 **geographyMultiLineString** 執行個體的 WKB 表示法。 *WKB_multilinestring* 是 **varbinary(max)** 運算式。  
  
 *SRID*  
 這是 **int** 運算式，表示要傳回之 **geographyMultiLineString** 執行個體的空間參考識別碼 (SRID)。  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**geography**  
  
 CLR 傳回類型：**SqlGeography**  
  
 OGC 類型：**MultiLineString**  
  
## <a name="remarks"></a>Remarks  
 如果輸入的格式不正確，這個方法將會擲回 **FormatException**。  
  
## <a name="examples"></a>範例  
 下列範例會使用 `STMLineFromWKB()` 建立 `geography` 執行個體。  
  
```  
DECLARE @g geography;  
SET @g = geography::STMLineFromWKB(0x010500000002000000010200000005000000F4FDD478E9965EC0DD24068195D3474083C0CAA145965EC0508D976E12D3474083C0CAA145965EC04E62105839D44740F4FDD478E9965EC04E62105839D44740F4FDD478E9965EC0DD24068195D34740010200000005000000022B8716D9965EC0C1CAA145B6D34740022B8716D9965EC06ABC749318D447407593180456965EC06ABC749318D447407593180456965EC03333333333D34740022B8716D9965EC0C1CAA145B6D34740, 4326);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>另請參閱  
 [OGC 靜態地理方法](../../t-sql/spatial-geography/ogc-static-geography-methods.md)  
  
  
