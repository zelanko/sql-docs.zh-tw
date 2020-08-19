---
description: 描述參數
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a41bee40403cc3562c41ccc13a15c706a0772e27
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476750"
---
# <a name="describing-parameters"></a>描述參數
**SQLBindParameter** 具有可描述參數的引數：其 SQL 型別、精確度和小數位數。 驅動程式會使用此資訊或 *中繼資料，* 將參數值轉換成資料來源所需的型別。 乍看之下，驅動程式的位置可能會比應用程式更清楚地知道參數中繼資料;畢竟，驅動程式可以輕鬆地探索結果集資料行的中繼資料。 結果如此，就不會發生這種情況。 首先，大部分的資料來源都不會提供驅動程式探索參數中繼資料的方法。 其次，大部分的應用程式都已經知道中繼資料。  
  
 如果在應用程式中硬式編碼的 SQL 語句，則應用程式寫入器已經知道每個參數的型別。 如果 SQL 語句是由應用程式在執行時間所建立，應用程式可以在建立語句時判斷中繼資料。 例如，當應用程式建立子句時  
  
```  
WHERE OrderID = ?  
```  
  
 它可以針對 [訂單] 資料行呼叫 **SQLColumns** 。  
  
 應用程式無法輕易判斷參數中繼資料的唯一情況，就是當使用者輸入參數化語句時。 在此情況下，應用程式會呼叫 **SQLPrepare** 來準備語句、 **SQLNumParams** 來判斷參數的數目，以及用來描述每個參數的 **SQLDescribeParam** 。 不過，如先前所述，大部分的資料來源都不會提供驅動程式探索參數中繼資料的方法，因此不會廣泛支援 **SQLDescribeParam** 。
