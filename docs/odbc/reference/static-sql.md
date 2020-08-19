---
description: 靜態 SQL
title: 靜態 SQL |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- static SQL [ODBC]
- SQL [ODBC], embedded SQL
- SQL statements [ODBC], embedded SQL
- SQL statements [ODBC], static SQL
- embedded SQL [ODBC]
- SQL [ODBC], static SQL
ms.assetid: 667d92ec-fed9-4028-81d4-bb9ba867356a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 19c4ec3454a5d5891a87203fe8c7aeaff21b239b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88428980"
---
# <a name="static-sql"></a>靜態 SQL
內嵌 sql [範例](../../odbc/reference/embedded-sql-example.md) 中所顯示的內嵌 sql 稱為靜態 sql。 它稱為靜態 SQL，因為程式中的 SQL 語句是靜態的;也就是說，每次執行程式時都不會變更。 如上一節所述，編譯器的其餘部分時，會編譯這些語句。  
  
 靜態 SQL 在許多情況下都能順利運作，而且可以用於任何可在程式設計時間決定資料存取的應用程式。 例如，「訂單輸入」程式一律會使用相同的語句來插入新訂單，而航空公司保留系統一律會使用相同的語句，將基座的狀態從「可用」變更為「保留」。 每個語句都會透過使用主機變數進行一般化;您可以在銷售訂單中插入不同的值，而且可以保留不同的基座。 由於這類語句可以在程式中進行硬式編碼，因此這類程式有一項優點，就是在編譯時期，語句只需要剖析、驗證和優化一次。 這會產生相對快速的程式碼。
