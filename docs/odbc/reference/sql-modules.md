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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 30c116878049c4f6a8f36e988731ab641e03c6d7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63232769"
---
# <a name="sql-modules"></a>SQL 模組
將 SQL 陳述式傳送至 DBMS 的第二個技巧是透過模組。 簡單地說，模組會包含群組的程序，從主應用程式的程式設計語言呼叫。 每個程序包含單一的 SQL 陳述式，且資料會傳遞與程序參數。  
  
 模組可以視為物件程式庫連結至應用程式程式碼。 不過，完全如何程序和應用程式的其餘部分連結是視實作而定。 比方說，無法編譯成物件的程式碼的程序，以及直接連結到應用程式程式碼、 無法編譯並儲存在 DBMS 和呼叫以存取計劃識別碼放在應用程式的程式碼，或它們無法在執行階段解譯。  
  
 模組的主要優點是它們完全不同的程式設計語言的 SQL 陳述式。 理論上來說，它應該是可以變更其中一個，而不需要變更其他，並只將它們重新連結。
