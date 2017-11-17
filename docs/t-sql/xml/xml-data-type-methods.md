---
title: "xml 資料類型方法 |Microsoft 文件"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|xml
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- xml data type [SQL Server], methods
- methods [XML in SQL Server]
ms.assetid: d112b9c9-be9f-435c-a9e6-d21b65778fb7
caps.latest.revision: 32
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: fcf16bd9b71f27ab91fb02bbfd7bb7625185b44e
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="xml-data-type-methods"></a>xml 資料類型方法
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  您可以使用**xml**資料類型方法來查詢儲存在變數或資料行中的 XML 執行個體**xml**型別。 本節中的主題描述如何使用**xml**資料類型方法。  
  
## <a name="in-this-section"></a>本節內容  
  
|主題|Description|  
|-----------|-----------------|  
|[查詢 &#40; &#41;方法 &#40; xml 資料類型 &#41;](../../t-sql/xml/query-method-xml-data-type.md)|描述如何使用 query() 方法來查詢 XML 執行個體。|  
|[值 &#40; &#41;方法 &#40; xml 資料類型 &#41;](../../t-sql/xml/value-method-xml-data-type.md)|描述如何使用 value() 方法來擷取 XML 執行個體中的 SQL 類型值。|  
|[存在 &#40; &#41;方法 &#40; xml 資料類型 &#41;](../../t-sql/xml/exist-method-xml-data-type.md)|描述如何使用 exist() 方法來判斷查詢是否傳回非空的結果。|  
|[修改 &#40; &#41;方法 &#40; xml 資料類型 &#41;](../../t-sql/xml/modify-method-xml-data-type.md)|描述如何使用 modify （） 方法來指定[XML 資料修改語言 &#40;XML DML &#41;](../../t-sql/xml/xml-data-modification-language-xml-dml.md)陳述式來執行更新。|  
|[節點 &#40; &#41;方法 &#40; xml 資料類型 &#41;](../../t-sql/xml/nodes-method-xml-data-type.md)|描述如何使用 nodes() 方法將 XML 切割成多個資料列，這樣會將 XML 文件的部分傳播到資料列集中。|  
|[在 XML 資料中繫結關聯式資料](../../t-sql/xml/binding-relational-data-inside-xml-data.md)|描述如何繫結 XML 內的非 XML 資料。|  
|[使用 xml 資料類型方法的指導方針](../../t-sql/xml/guidelines-for-using-xml-data-type-methods.md)|描述使用的指導方針**xml**資料類型方法。|  
  
 您可以使用使用者自訂類型方法叫用語法以呼叫這些方法。 例如：  
  
```  
SELECT XmlCol.query(' ... ')  
FROM   Table  
```  
  
> [!NOTE]  
>  **Xml**資料類型方法**query （)**， **value （)**，和**exist （)**針對 NULL XML 執行個體執行時傳回 NULL。 此外， **modify （)**不會傳回任何項目，但**nodes （)**含有 NULL 輸入會傳回資料列集和空白資料列集。  
  
## <a name="see-also"></a>另請參閱  
 [比較具類型的 XML 與不具類型的 XML](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [建立 XML 資料的執行個體](../../relational-databases/xml/create-instances-of-xml-data.md)  
  
  

