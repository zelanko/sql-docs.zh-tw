---
title: xml 資料類型方法 | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: sql-database
ms.component: t-sql|xml
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- xml data type [SQL Server], methods
- methods [XML in SQL Server]
ms.assetid: d112b9c9-be9f-435c-a9e6-d21b65778fb7
caps.latest.revision: 32
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b788282072088b4c9ee98b27b6f4ce3fb2b923c6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "33070345"
---
# <a name="xml-data-type-methods"></a>xml 資料類型方法
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  您可以使用 **xml** 資料類型方法來查詢儲存在 **xml** 類型之變數或資料行中的 XML 執行個體。 本節中的主題會描述如何使用 **xml** 資料類型方法。  
  
## <a name="in-this-section"></a>本節內容  
  
|主題|描述|  
|-----------|-----------------|  
|[query&#40;&#41; 方法 &#40;xml 資料類型&#41;](../../t-sql/xml/query-method-xml-data-type.md)|描述如何使用 query() 方法來查詢 XML 執行個體。|  
|[value&#40;&#41; 方法 &#40;xml 資料類型&#41;](../../t-sql/xml/value-method-xml-data-type.md)|描述如何使用 value() 方法來擷取 XML 執行個體中的 SQL 類型值。|  
|[exist&#40;&#41; 方法 &#40;xml 資料類型&#41;](../../t-sql/xml/exist-method-xml-data-type.md)|描述如何使用 exist() 方法來判斷查詢是否傳回非空的結果。|  
|[modify&#40;&#41; 方法 &#40;xml 資料類型&#41;](../../t-sql/xml/modify-method-xml-data-type.md)|描述如何使用 modify() 方法來指定 [XML 資料修改語言 &#40;XML DML&#41;](../../t-sql/xml/xml-data-modification-language-xml-dml.md) 陳述式以執行更新。|  
|[nodes&#40;&#41; 方法 &#40;xml 資料類型&#41;](../../t-sql/xml/nodes-method-xml-data-type.md)|描述如何使用 nodes() 方法將 XML 切割成多個資料列，這樣會將 XML 文件的部分傳播到資料列集中。|  
|[在 XML 資料中繫結關聯式資料](../../t-sql/xml/binding-relational-data-inside-xml-data.md)|描述如何繫結 XML 內的非 XML 資料。|  
|[使用 xml 資料類型方法的指導方針](../../t-sql/xml/guidelines-for-using-xml-data-type-methods.md)|描述使用 **xml** 資料類型方法的指導方針。|  
  
 您可以使用使用者自訂類型方法叫用語法以呼叫這些方法。 例如：  
  
```  
SELECT XmlCol.query(' ... ')  
FROM   Table  
```  
  
> [!NOTE]  
>  如果針對 NULL XML 執行個體執行，**xml** 資料類型方法 **query()**、**value()** 和 **exist()** 會傳回 NULL。 另外，**modify()** 並不會傳回任何內容，但是 **nodes()** 則會傳回資料列集以及含有 NULL 輸入的空資料列集。  
  
## <a name="see-also"></a>另請參閱  
 [比較具類型的 XML 與不具類型的 XML](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [建立 XML 資料的執行個體](../../relational-databases/xml/create-instances-of-xml-data.md)  
  
  
