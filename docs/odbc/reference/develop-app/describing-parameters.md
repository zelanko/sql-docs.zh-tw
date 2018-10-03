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
manager: craigg
ms.openlocfilehash: 1bc752afc0cb5214e629a343c35464e612b57c36
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47808966"
---
# <a name="describing-parameters"></a>描述參數
**SQLBindParameter**包含描述參數的引數： 其 SQL 類型、 有效位數和小數位數。 驅動程式會使用這項資訊，或是*中繼資料，* 將參數值轉換成所需的資料來源類型。 第一眼，它看起來的驅動程式是有利的位置，來了解應用程式; 以外的參數中繼資料中畢竟，驅動程式可以輕易找出中繼資料的結果集資料行。 其實，這不是如此。 首先，大部分的資料來源未提供的驅動程式，以探索參數中繼資料的方式。 第二個，大部分的應用程式已知的中繼資料。  
  
 如果 SQL 陳述式是硬式編碼應用程式中，應用程式寫入器已經知道每個參數的型別。 如果應用程式在執行階段建構 SQL 陳述式時，應用程式可以判斷中繼資料，與建立陳述式。 例如，當應用程式會建構子句  
  
```  
WHERE OrderID = ?  
```  
  
 它可以呼叫**SQLColumns** OrderID 資料行。  
  
 只有這種情況，並在其中應用程式無法輕易判斷參數中繼資料時，使用者輸入的參數化陳述式。 在此情況下，應用程式會呼叫**SQLPrepare**準備陳述式時， **SQLNumParams**判斷幾個參數，並**SQLDescribeParam**來描述每個參數。 不過，已前面有提到，大部分的資料來源未提供驅動程式，因此探索參數中繼資料，讓**SQLDescribeParam**尚未廣泛支援。
