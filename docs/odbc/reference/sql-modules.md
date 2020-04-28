---
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
ms.openlocfilehash: 351d1c6a34413b385bd76dfebb009b34c4c0f150
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81280420"
---
# <a name="sql-modules"></a>SQL 模組
將 SQL 語句傳送至 DBMS 的第二種方法是透過模組。 簡單地說，模組是由一組程式所組成，這些程式是從主機程式設計語言呼叫。 每個程式都包含單一 SQL 語句，而資料會透過參數傳入和傳送。  
  
 模組可視為連結至應用程式程式碼的物件程式庫。 不過，與應用程式和其餘部分連結的確切方式，與執行相依。 例如，程式可以編譯成物件程式碼，並直接連結到應用程式的程式碼，它們可以編譯並儲存在 DBMS 上，並呼叫放置在應用程式代碼中的存取計畫識別碼，或是在執行時間加以解讀。  
  
 模組的主要優點是它們會從程式設計語言中明確分隔 SQL 語句。 理論上，應該可以變更其中一個，而不需要變更另一個，並直接重新連結它們。
