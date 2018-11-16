---
title: 資料存取子函式 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- data-accessor functions [XQuery]
ms.assetid: 31bad04f-7c74-4773-9f83-612704fdd21c
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: ca466042ba90915076b0be47f867d74c3ab86e68
ms.sourcegitcommit: 0f7cf9b7ab23df15624d27c129ab3a539e8b6457
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2018
ms.locfileid: "51292064"
---
# <a name="data-accessor-functions"></a>Data Accessor 函數
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  本節中的主題討論並提供 data-accessor 函數的範例程式碼。  
  
## <a name="understanding-fndata-fnstring-and-text"></a>了解 fn:data()、fn:string() 與 text()  
 XQuery 有一個函數**fn:data()** 節點，節點測試中擷取純量、 具類型值**text （)** 傳回文字節點和函式**fn: string**傳回節點的字串值。 它們的用法很容易混淆。 以下是在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中正確使用它們的指導方針。 XML 執行個體\<age > 12 \< /age > 用來舉例說明。  
  
-   不具類型的 XML：路徑運算式 /age/text() 會傳回文字節點 "12"。 函數 fn:data(/age) 會傳回字串值 "12"，而 fn:string(/age) 也是。  
  
-   具類型的 XML： 運算式 /age/text （） 傳回的任何簡單類型的靜態錯誤\<age > 項目。 在另一方面，fn:data(/age) 會傳回整數 12。 fn:string(/age) 會產生字串 "12"。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [string 函式&#40;XQuery&#41;](../xquery/data-accessor-functions-string-xquery.md)  
  
-   [資料函式&#40;XQuery&#41;](../xquery/data-accessor-functions-data-xquery.md)  
  
## <a name="see-also"></a>另請參閱  
 [路徑運算式&#40;XQuery&#41;](../xquery/path-expressions-xquery.md)  
  
  
