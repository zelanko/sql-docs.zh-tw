---
title: 針對 xml 資料類型的 XQuery 函數 |Microsoft Docs
description: 瞭解針對 xml 資料類型支援使用的 XQuery 函數。
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- XQuery, functions
- xml data type [SQL Server], XQuery
- functions [SQL Server], XQuery
ms.assetid: 8df0877d-a03f-4ca9-b84e-908c4bb42b5e
author: rothja
ms.author: jroth
ms.openlocfilehash: 8e92148b5a85ced147599eafe09156cf41c47021
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/14/2020
ms.locfileid: "92037011"
---
# <a name="xquery-functions-against-the-xml-data-type"></a>針對 xml 資料類型的 XQuery 函數
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  本主題及其子主題說明針對 **xml** 資料類型指定 XQuery 時可以使用的函數。 如需 W3C 規格，請參閱 [http://www.w3.org/TR/2004/WD-xpath-functions-20040723](https://go.microsoft.com/fwlink/?LinkId=4873) 。  
  
 XQuery 函數屬於 http://www.w3.org/2004/07/xpath-functions 命名空間。 W3C 規格會使用 "fn:" 命名空間前置詞，來描述這些函數。 使用函數時，您不需要明確地指定 "fn:" 命名空間前置詞。 由於此點以及為了能改善可讀性，所以在此份文件中通常不會使用命名空間前置詞。  
  
 下表列出針對 **xml**資料類型所支援的 XQuery 函數。  
  
|類別|函數名稱|  
|--------------|-------------------|  
|[數值的函數]()|[天花板](../xquery/numeric-values-functions-ceiling.md)|  
||[地板](../xquery/numeric-values-functions-floor.md)|  
||[輪](../xquery/numeric-values-functions-round.md)|  
|[字串值的相關 XQuery 函數]()|[concat](../xquery/functions-on-string-values-concat.md)|  
||[contains](../xquery/functions-on-string-values-contains.md)|  
||[substring](../xquery/functions-on-string-values-substring.md)|  
||[&#40;XQuery&#41;的小寫函數 ](../xquery/functions-on-string-values-lower-case.md)|  
||[字串-長度](../xquery/functions-on-string-values-string-length.md)|  
||[大寫函數 &#40;XQuery&#41;](../xquery/functions-on-string-values-upper-case.md)|  
|布林值相關函數|[not](../xquery/functions-on-boolean-values-not-function.md)|  
|[節點上的函數]()|[number](../xquery/functions-on-nodes-number.md)|  
||[local-name 函數 (XQuery)](../xquery/functions-on-nodes-local-name.md)|  
||[namespace-uri 函數 (XQuery)](../xquery/functions-on-nodes-namespace-uri.md)|  
|[內容函數]()|[last](../xquery/context-functions-last-xquery.md)|  
||[position](../xquery/context-functions-position-xquery.md)|  
|[序列的相關函數]()|[empty](../xquery/functions-on-sequences-empty.md)|  
||[distinct-values](../xquery/functions-on-sequences-distinct-values.md)|  
||[id 函數 (XQuery)](../xquery/functions-on-sequences-id.md)|  
|[&#40;XQuery&#41;的彙總函式 ]()|[計數](../xquery/aggregate-functions-count.md)|  
||[Avg](../xquery/aggregate-functions-avg.md)|  
||[min](../xquery/aggregate-functions-min.md)|  
||[max](../xquery/aggregate-functions-max.md)|  
||[sum](../xquery/aggregate-functions-sum.md)|  
|[&#40;XQuery&#41;的函式函數 ](../xquery/constructor-functions-xquery.md)|[建構函式](../xquery/constructor-functions-xquery.md)|  
|[Data Accessor 函數](../xquery/data-accessor-functions.md)|[string](../xquery/data-accessor-functions-string-xquery.md)|  
||[data](../xquery/data-accessor-functions-data-xquery.md)|  
|[&#40;XQuery&#41;的布林函式函數 ]()|[true 函數 (XQuery)](../xquery/boolean-constructor-functions-true-xquery.md)|  
||[false 函數 (XQuery)](../xquery/boolean-constructor-functions-false-xquery.md)|  
|[QNames &#40;XQuery&#41;的相關函數 ](./functions-related-to-qnames-expanded-qname.md)|[expanded-QName (XQuery)](../xquery/functions-related-to-qnames-expanded-qname.md)|  
||[local-name-from-QName (XQuery)](../xquery/functions-related-to-qnames-local-name-from-qname.md)|  
||[namespace-uri-from-QName (XQuery)](../xquery/functions-related-to-qnames-namespace-uri-from-qname.md)|  
|[SQL Server XQuery 擴充函數](./xquery-extension-functions-sql-column.md)|[sql： column ( # A1 函數 (XQuery) ](../xquery/xquery-extension-functions-sql-column.md)|  
||[sql：變數 ( # A1 函數 (XQuery) ](../xquery/xquery-extension-functions-sql-variable.md)|  
  
## <a name="see-also"></a>另請參閱  
 [xml 資料類型方法](../t-sql/xml/xml-data-type-methods.md)   
 [XQuery 語言參考 &#40;SQL Server&#41;](../xquery/xquery-language-reference-sql-server.md)   
 [XML 資料 &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)  
  
