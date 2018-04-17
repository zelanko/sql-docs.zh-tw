---
title: 描述參數 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQLBindParameter function [ODBC], describing parameters
ms.assetid: 118d0f47-2afd-4955-bb47-38b1e2c2f38f
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b90b71a5e327e894329ca8474e8edff5740d8826
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="describing-parameters"></a>描述參數
**SQLBindParameter**包含描述參數的引數： 其 SQL 類型、 有效位數和小數位數。 驅動程式會使用這項資訊，或*中繼資料，*將參數值轉換成所需的資料來源類型。 第一眼看起來，看起來的驅動程式是較佳位置知道參數中繼資料，以比應用程式。畢竟，驅動程式可以輕鬆地探索中繼資料的結果集資料行。 結果顯示，但這不是大小寫。 首先，大部分的資料來源未提供的驅動程式來探索參數中繼資料的方式。 第二個，大部分的應用程式已經知道中繼資料。  
  
 如果 SQL 陳述式是硬式編碼應用程式中，應用程式寫入器已經知道每個參數的型別。 如果應用程式在執行階段建構 SQL 陳述式時，應用程式可以判斷中繼資料，當它建立陳述式。 例如，當應用程式建構子句  
  
```  
WHERE OrderID = ?  
```  
  
 它可以呼叫**SQLColumns** OrderID 資料行。  
  
 在其中應用程式無法輕易地判斷參數中繼資料的唯一情況是當使用者輸入的參數化陳述式。 在此情況下，應用程式呼叫**SQLPrepare**準備陳述式時， **SQLNumParams**來判斷參數的數目和**SQLDescribeParam**來描述每個參數。 不過，如同先前所說明，大部分的資料來源未提供的方式來探索參數中繼資料，因此驅動程式**SQLDescribeParam**尚未廣泛支援。
