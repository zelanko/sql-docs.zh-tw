---
title: 針對 xml 資料類型的 XQuery 函數 |Microsoft Docs
description: 瞭解支援用於 xml 資料類型的 XQuery 函數。
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
ms.openlocfilehash: ad25db1aa5a10039bc80766b30e1d2ba478df123
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85730984"
---
# <a name="xquery-functions-against-the-xml-data-type"></a>針對 xml 資料類型的 XQuery 函數
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  本主題及其子主題描述您在針對**xml**資料類型指定 XQuery 時可以使用的函數。 如需 W3C 規格，請參閱 [http://www.w3.org/TR/2004/WD-xpath-functions-20040723](https://go.microsoft.com/fwlink/?LinkId=4873) 。  
  
 XQuery 函數屬於 http://www.w3.org/2004/07/xpath-functions 命名空間。 W3C 規格會使用 "fn:" 命名空間前置詞，來描述這些函數。 使用函數時，您不需要明確地指定 "fn:" 命名空間前置詞。 由於此點以及為了能改善可讀性，所以在此份文件中通常不會使用命名空間前置詞。  
  
 下表列出針對**xml**資料類型所支援的 XQuery 函數。  
  
|類別|函數名稱|  
|--------------|-------------------|  
|[數值的函數](https://msdn.microsoft.com/library/d5740a32-b174-43b9-b64d-1cc6edc50cff)|[向上](../xquery/numeric-values-functions-ceiling.md)|  
||[車間](../xquery/numeric-values-functions-floor.md)|  
||[進行](../xquery/numeric-values-functions-round.md)|  
|[字串值的相關 XQuery 函數](https://msdn.microsoft.com/library/2dccefef-5d90-4f56-bda7-4c1954d8a730)|[concat](../xquery/functions-on-string-values-concat.md)|  
||[contains](../xquery/functions-on-string-values-contains.md)|  
||[substring](../xquery/functions-on-string-values-substring.md)|  
||[小寫函數 &#40;XQuery&#41;](../xquery/functions-on-string-values-lower-case.md)|  
||[字串長度](../xquery/functions-on-string-values-string-length.md)|  
||[大寫函數 &#40;XQuery&#41;](../xquery/functions-on-string-values-upper-case.md)|  
|布林值相關函數|[not](../xquery/functions-on-boolean-values-not-function.md)|  
|[節點上的函式](https://msdn.microsoft.com/library/09a8affa-3341-4f50-aebc-fdf529e00c08)|[number](../xquery/functions-on-nodes-number.md)|  
||[local-name 函數 (XQuery)](../xquery/functions-on-nodes-local-name.md)|  
||[namespace-uri 函數 (XQuery)](../xquery/functions-on-nodes-namespace-uri.md)|  
|[內容函式](https://msdn.microsoft.com/library/f7d8af33-9de9-450c-a667-23dee3129b5f)|[last](../xquery/context-functions-last-xquery.md)|  
||[position](../xquery/context-functions-position-xquery.md)|  
|[序列的相關函數](https://msdn.microsoft.com/library/672d2795-53ab-49c2-bf24-bc81a47ecd3f)|[empty](../xquery/functions-on-sequences-empty.md)|  
||[distinct-values](../xquery/functions-on-sequences-distinct-values.md)|  
||[id 函數 (XQuery)](../xquery/functions-on-sequences-id.md)|  
|[&#40;XQuery&#41;的彙總函式](https://msdn.microsoft.com/library/be647ef1-291e-4a5d-ab18-07c759efe176)|[計數](../xquery/aggregate-functions-count.md)|  
||[avg](../xquery/aggregate-functions-avg.md)|  
||[min](../xquery/aggregate-functions-min.md)|  
||[max](../xquery/aggregate-functions-max.md)|  
||[sum](../xquery/aggregate-functions-sum.md)|  
|[&#40;XQuery&#41;的函式函數](../xquery/constructor-functions-xquery.md)|[建構函式](../xquery/constructor-functions-xquery.md)|  
|[Data Accessor 函數](../xquery/data-accessor-functions.md)|[string](../xquery/data-accessor-functions-string-xquery.md)|  
||[資料](../xquery/data-accessor-functions-data-xquery.md)|  
|[&#40;XQuery&#41;的布林函式函數](https://msdn.microsoft.com/library/fa907f39-d4b7-4495-b829-c788928e0f64)|[true 函數 (XQuery)](../xquery/boolean-constructor-functions-true-xquery.md)|  
||[false 函數 (XQuery)](../xquery/boolean-constructor-functions-false-xquery.md)|  
|[與 QNames &#40;XQuery&#41;相關的函數](https://msdn.microsoft.com/library/7e07eb26-f551-4b63-ab77-861684faff71)|[expanded-QName (XQuery)](../xquery/functions-related-to-qnames-expanded-qname.md)|  
||[local-name-from-QName (XQuery)](../xquery/functions-related-to-qnames-local-name-from-qname.md)|  
||[namespace-uri-from-QName (XQuery)](../xquery/functions-related-to-qnames-namespace-uri-from-qname.md)|  
|[SQL Server XQuery 擴充函數](https://msdn.microsoft.com/library/4bc5d499-5fec-4c3f-b11e-5ab5ef9d8f97)|[sql： column （）函數（XQuery）](../xquery/xquery-extension-functions-sql-column.md)|  
||[sql： variable （）函數（XQuery）](../xquery/xquery-extension-functions-sql-variable.md)|  
  
## <a name="see-also"></a>另請參閱  
 [xml 資料類型方法](../t-sql/xml/xml-data-type-methods.md)   
 [XQuery 語言參考 &#40;SQL Server&#41;](../xquery/xquery-language-reference-sql-server.md)   
 [XML 資料 &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)  
  
  
