---
title: 針對 xml 資料類型的 XQuery 函數 |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 6a7527fe3fb4e250e0cf884e17ee6e53eeba7b8b
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2019
ms.locfileid: "56042949"
---
# <a name="xquery-functions-against-the-xml-data-type"></a>針對 xml 資料類型的 XQuery 函數
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  本主題及其子主題說明指定針對 XQuery 時，您可以使用的函式**xml**資料型別。 如需 W3C 規格，請參閱[ http://www.w3.org/TR/2004/WD-xpath-functions-20040723 ](https://go.microsoft.com/fwlink/?LinkId=4873)。  
  
 XQuery 函數屬於 http://www.w3.org/2004/07/xpath-functions命名空間。 W3C 規格會使用 "fn:" 命名空間前置詞，來描述這些函數。 使用函數時，您不需要明確地指定 "fn:" 命名空間前置詞。 由於此點以及為了能改善可讀性，所以在此份文件中通常不會使用命名空間前置詞。  
  
 下表列出支援的 XQuery 函式**xml**資料型別。  
  
|類別目錄|函數名稱|  
|--------------|-------------------|  
|[針對數值的函式](https://msdn.microsoft.com/library/d5740a32-b174-43b9-b64d-1cc6edc50cff)|[ceiling](../xquery/numeric-values-functions-ceiling.md)|  
||[floor](../xquery/numeric-values-functions-floor.md)|  
||[round](../xquery/numeric-values-functions-round.md)|  
|[字串值的相關 XQuery 函數](https://msdn.microsoft.com/library/2dccefef-5d90-4f56-bda7-4c1954d8a730)|[concat](../xquery/functions-on-string-values-concat.md)|  
||[包含](../xquery/functions-on-string-values-contains.md)|  
||[substring](../xquery/functions-on-string-values-substring.md)|  
||[lower-case 函數&#40;XQuery&#41;](../xquery/functions-on-string-values-lower-case.md)|  
||[string-length](../xquery/functions-on-string-values-string-length.md)|  
||[upper-case 函數&#40;XQuery&#41;](../xquery/functions-on-string-values-upper-case.md)|  
|布林值相關函數|[not](../xquery/functions-on-boolean-values-not-function.md)|  
|[在節點上的函式](https://msdn.microsoft.com/library/09a8affa-3341-4f50-aebc-fdf529e00c08)|[number](../xquery/functions-on-nodes-number.md)|  
||[local-name 函數 (XQuery)](../xquery/functions-on-nodes-local-name.md)|  
||[namespace-uri 函數 (XQuery)](../xquery/functions-on-nodes-namespace-uri.md)|  
|[內容函式](https://msdn.microsoft.com/library/f7d8af33-9de9-450c-a667-23dee3129b5f)|[last](../xquery/context-functions-last-xquery.md)|  
||[position](../xquery/context-functions-position-xquery.md)|  
|[在序列上的函式](https://msdn.microsoft.com/library/672d2795-53ab-49c2-bf24-bc81a47ecd3f)|[empty](../xquery/functions-on-sequences-empty.md)|  
||[distinct-values](../xquery/functions-on-sequences-distinct-values.md)|  
||[id 函數 (XQuery)](../xquery/functions-on-sequences-id.md)|  
|[彙總函式&#40;XQuery&#41;](https://msdn.microsoft.com/library/be647ef1-291e-4a5d-ab18-07c759efe176)|[計數](../xquery/aggregate-functions-count.md)|  
||[avg](../xquery/aggregate-functions-avg.md)|  
||[min](../xquery/aggregate-functions-min.md)|  
||[max](../xquery/aggregate-functions-max.md)|  
||[sum](../xquery/aggregate-functions-sum.md)|  
|[建構函式&#40;XQuery&#41;](../xquery/constructor-functions-xquery.md)|[建構函式](../xquery/constructor-functions-xquery.md)|  
|[資料存取子函式](../xquery/data-accessor-functions.md)|[string](../xquery/data-accessor-functions-string-xquery.md)|  
||[data](../xquery/data-accessor-functions-data-xquery.md)|  
|[布林建構函式&#40;XQuery&#41;](https://msdn.microsoft.com/library/fa907f39-d4b7-4495-b829-c788928e0f64)|[true 函數 (XQuery)](../xquery/boolean-constructor-functions-true-xquery.md)|  
||[false 函數 (XQuery)](../xquery/boolean-constructor-functions-false-xquery.md)|  
|[與 QNames 相關的函式&#40;XQuery&#41;](https://msdn.microsoft.com/library/7e07eb26-f551-4b63-ab77-861684faff71)|[擴充 QName (XQuery)](../xquery/functions-related-to-qnames-expanded-qname.md)|  
||[local-name-from-QName (XQuery)](../xquery/functions-related-to-qnames-local-name-from-qname.md)|  
||[namespace-uri-from-QName (XQuery)](../xquery/functions-related-to-qnames-namespace-uri-from-qname.md)|  
|[SQL Server XQuery 擴充函式](https://msdn.microsoft.com/library/4bc5d499-5fec-4c3f-b11e-5ab5ef9d8f97)|[sql: column 函數 (XQuery)](../xquery/xquery-extension-functions-sql-column.md)|  
||[（） 函數 (XQuery)](../xquery/xquery-extension-functions-sql-variable.md)|  
  
## <a name="see-also"></a>另請參閱  
 [xml 資料類型方法](../t-sql/xml/xml-data-type-methods.md)   
 [XQuery 語言參考 &#40;SQL Server&#41;](../xquery/xquery-language-reference-sql-server.md)   
 [XML 資料 &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)  
  
  
