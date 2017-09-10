---
title: "資料存取子函式 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- data-accessor functions [XQuery]
ms.assetid: 31bad04f-7c74-4773-9f83-612704fdd21c
caps.latest.revision: 30
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 456d359fd407e305bc8bfb3b85bd29b7bada8382
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="data-accessor-functions"></a>Data Accessor 函數
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  本節中的主題討論並提供 data-accessor 函數的範例程式碼。  
  
## <a name="understanding-fndata-fnstring-and-text"></a>了解 fn:data()、fn:string() 與 text()  
 XQuery 有一個函數**fn:data()**節點，節點測試中擷取純量、 具類型值**text （)**傳回文字節點和函式**fn: string**傳回節點的字串值。 它們的用法很容易混淆。 以下是在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中正確使用它們的指導方針。 XML 執行個體\<age > 12 \< /age > 用來舉例說明。  
  
-   不具類型的 XML：路徑運算式 /age/text() 會傳回文字節點 "12"。 函數 fn:data(/age) 會傳回字串值 "12"，而 fn:string(/age) 也是。  
  
-   具類型的 XML： 運算式 /age/text （） 傳回靜態錯誤的任何簡單類型\<age > 項目。 在另一方面，fn:data(/age) 會傳回整數 12。 fn:string(/age) 會產生字串 "12"。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [字串函數 &#40;XQuery &#41;](../xquery/data-accessor-functions-string-xquery.md)  
  
-   [data 函數 &#40;XQuery &#41;](../xquery/data-accessor-functions-data-xquery.md)  
  
## <a name="see-also"></a>另請參閱  
 [路徑運算式 &#40;XQuery &#41;](../xquery/path-expressions-xquery.md)  
  
  
