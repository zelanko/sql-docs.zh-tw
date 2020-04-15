---
title: 描述參數 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLBindParameter function [ODBC], describing parameters
ms.assetid: 118d0f47-2afd-4955-bb47-38b1e2c2f38f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f4d9284294707da0a469bf75ff9812ad5f7855bb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305939"
---
# <a name="describing-parameters"></a>描述參數
**SQLBind參數**具有描述參數的參數:其 SQL 類型、精度和縮放。 驅動程式使用此資訊或*元資料*將參數值轉換為數據源所需的類型。 乍一看,驅動程式似乎比應用程式更瞭解參數元數據;畢竟,驅動程式可以輕鬆地發現結果集列的元數據。 事實證明,情況並非如此。 首先,大多數數據源不為驅動程式提供發現參數元數據的方法。 其次,大多數應用程式已經知道元數據。  
  
 如果 SQL 語句在應用程式中是硬編碼的,則應用程式編寫器已經知道每個參數的類型。 如果 SQL 語句由應用程式在運行時建構,則應用程式可以在生成語句時確定元數據。 例如,當應用程式建構子句時  
  
```  
WHERE OrderID = ?  
```  
  
 它可以為 OrderID 列調用**SQLColumn。**  
  
 應用程式無法輕鬆確定參數元數據的唯一情況是使用者輸入參數化語句。 在這種情況下,應用程式調用**SQLPrepare**來準備敘述 **,SQLNumParams**來確定參數數 **,SQLDescribeParam**來描述每個參數。 但是,如前所述,大多數數據源不為驅動程式提供發現參數元數據的方法,因此**SQLDescribeParam**並不得到廣泛支援。
