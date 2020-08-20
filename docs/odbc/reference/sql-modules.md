---
description: SQL 模組
title: SQL 模組 |Microsoft Docs
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
ms.openlocfilehash: 39739ed5469b791cd0faf3df3946bebeb5d21761
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499641"
---
# <a name="sql-modules"></a>SQL 模組
將 SQL 語句傳送至 DBMS 的第二個技巧是透過模組。 簡單來說，模組是由一組程式所組成，這些程式是從主機程式設計語言呼叫。 每個程式都包含單一 SQL 語句，並透過參數在程式之間傳遞資料。  
  
 您可以將模組視為連結至應用程式程式碼的物件程式庫。 不過，程式和應用程式其餘部分的連結方式，完全取決於它的執行方式。 例如，程式可以編譯為物件程式碼，並直接連結至應用程式程式碼，它們可以在 DBMS 上進行編譯和儲存，並呼叫以存取放置在應用程式程式碼中的計畫識別碼，或在執行時間加以解讀。  
  
 模組的主要優點是它們會將 SQL 語句與程式設計語言完全分開。 理論上，應該可以在不變更另一個的情況下變更，而只需重新連結。
