---
title: 引號識別碼 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], quoted identifiers
- quoted identifiers [ODBC]
ms.assetid: 729ba55f-743b-4a04-8c39-ac0a9914211d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0c03fa8bbc059566288997b29c899056f26de252
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81282001"
---
# <a name="quoted-identifiers"></a>引號識別碼
在 SQL 語句中，包含特殊字元或符合關鍵字的識別碼必須括在*識別碼引號字元*中;以這類字元括住的識別碼稱為*引號識別碼*（在 SQL-92 中也稱為*分隔識別碼*）。 例如，在下列**SELECT**語句中，帳戶應付的識別碼會加上引號：  
  
```  
SELECT * FROM "Accounts Payable"  
```  
  
 用來括住識別碼的原因是要讓語句剖析或是。 例如，如果在上一個語句中的帳戶未加上引號，則剖析器會假設有兩個數據表、帳戶和應付法，並傳回不是以逗號分隔的語法錯誤。 識別碼引號字元是驅動程式特有的，而且會使用**SQLGetInfo**中的 SQL_IDENTIFIER_QUOTE_CHAR 選項來抓取。 系統會使用**SQLGetInfo**中的 SQL_SPECIAL_CHARACTERS 和 SQL_KEYWORDS 選項來抓取特殊字元和關鍵字的清單。  
  
 為了安全起見，互通的應用程式通常會將所有識別碼加上引號，但虛擬資料行除外，例如 Oracle 中的 ROWID 資料行。 **SQLSpecialColumns**會傳回虛擬資料行的清單。 此外，如果有應用程式特定的限制，在物件名稱中可能出現特殊字元，則最適合互通的應用程式不要在這些位置使用特殊字元。
