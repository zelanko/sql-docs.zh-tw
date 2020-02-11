---
title: 描述參數 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2d32e5212ba1ba28262d871498f2974485d38233
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68040024"
---
# <a name="describing-parameters"></a>描述參數
**SQLBindParameter**具有可描述參數的引數：其 SQL 類型、有效位數和小數位數。 驅動程式會使用這項資訊或*中繼資料，* 將參數值轉換成資料來源所需的類型。 乍一眼，驅動程式可能會比應用程式更能知道參數中繼資料的位置;畢竟，驅動程式可以輕鬆地探索結果集資料行的中繼資料。 事實上，這種情況並非如此。 首先，大部分的資料來源都不會提供驅動程式探索參數中繼資料的方法。 第二，大部分的應用程式都已經知道中繼資料了。  
  
 如果 SQL 語句在應用程式中為硬式編碼，應用程式寫入器已經知道每個參數的類型。 如果 SQL 語句是由應用程式在執行時間所建立，則應用程式可以在建立語句時判斷中繼資料。 例如，當應用程式建立子句時  
  
```  
WHERE OrderID = ?  
```  
  
 它可以呼叫**SQLColumns**作為 [訂單] 資料行。  
  
 唯一的情況是當使用者輸入參數化語句時，應用程式無法輕易地判斷參數中繼資料。 在此情況下，應用程式會呼叫**SQLPrepare**來準備語句、 **SQLNumParams**以判斷參數的數目，以及**SQLDescribeParam**來描述每個參數。 不過，如先前所述，大部分的資料來源都不會提供驅動程式探索參數中繼資料的方法，因此不會廣泛支援**SQLDescribeParam** 。
