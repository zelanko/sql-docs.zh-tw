---
title: 資料存取子函式 |Microsoft Docs
description: 瞭解如何使用 XQuery 資料存取子函數 fn： data （）、fn： string （）和 text （）。
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
ms.openlocfilehash: d25fa2236feb02ba8ed726dc56b946dc09350d1c
ms.sourcegitcommit: 5c7634b007f6808c87094174b80376cb20545d5f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84881888"
---
# <a name="data-accessor-functions"></a>Data Accessor 函數
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  本節中的主題討論並提供 data-accessor 函數的範例程式碼。  
  
## <a name="understanding-fndata-fnstring-and-text"></a>了解 fn:data()、fn:string() 與 text()  
 XQuery 具有函數**fn： data （）** ，可從節點解壓縮純量、具類型的值、節點測試**文字（）** 以傳回文位元組點，以及函式**fn： string （）** ，可傳回節點的字串值。 它們的用法很容易混淆。 以下是在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中正確使用它們的指導方針。 XML 實例 \<age> 12 \</age> 是用來做為說明之用。  
  
-   不具類型的 XML：路徑運算式 /age/text() 會傳回文字節點 "12"。 函數 fn:data(/age) 會傳回字串值 "12"，而 fn:string(/age) 也是。  
  
-   具類型的 XML：運算式/age/text （）會傳回任何簡單類型專案的靜態錯誤 \<age> 。 在另一方面，fn:data(/age) 會傳回整數 12。 fn:string(/age) 會產生字串 "12"。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [string 函數 &#40;XQuery&#41;](../xquery/data-accessor-functions-string-xquery.md)  
  
-   [&#40;XQuery&#41;的資料函數](../xquery/data-accessor-functions-data-xquery.md)  
  
## <a name="see-also"></a>另請參閱  
 [&#40;XQuery&#41;的路徑運算式](../xquery/path-expressions-xquery.md)  
  
  
