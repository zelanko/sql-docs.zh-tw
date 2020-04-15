---
title: SQL 模組 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL modules [ODBC]
- sending SQL statements to DBMS [ODBC]
- SQL [ODBC], modules
- modules [ODBC]
- SQL statements [ODBC], modules
ms.assetid: 07551472-87ee-4765-951f-1364ed32f0c0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 351d1c6a34413b385bd76dfebb009b34c4c0f150
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280420"
---
# <a name="sql-modules"></a>SQL 模組
向 DBMS 發送 SQL 語句的第二種技術是通過模組。 簡而言之,模組由一組過程組成,這些過程從主機程式設計語言調用。 每個過程都包含一個 SQL 語句,數據通過參數傳入過程並從過程傳遞。  
  
 模組可以視為連結到應用程式代碼的物件庫。 但是,過程和應用程式的其餘部分的關聯方式與實現有關。 例如,過程可以編譯為對象代碼並直接連結到應用程式代碼,可以編譯並存儲在 DBMS 上,並調用應用程式代碼中放置的訪問計劃標識符,也可以在運行時對其進行解釋。  
  
 模組的主要優點是它們將 SQL 語句與程式設計語言完全分開。 從理論上講,應該可以改變一個而不改變另一個,只是重新連結他們。
