---
title: 引號識別項 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b0a81237eddd4836394cc9797a79690ba4b49a35
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47769046"
---
# <a name="quoted-identifiers"></a>引號識別碼
SQL 陳述式中包含特殊字元或多個相符項目關鍵字的識別項必須括住*識別項的引號字元*; 這類字元括住的識別項稱為*引號識別項*(也稱為*分隔識別碼*以 SQL-92)。 例如，Accounts Payable 識別碼已加上引號下列**選取**陳述式：  
  
```  
SELECT * FROM "Accounts Payable"  
```  
  
 引號識別項的原因是讓剖析陳述式。 例如，如果帳款未加引號的前一個陳述式中，剖析器會假定有兩個資料表的帳戶 」 和 「 應付帳款，並傳回語法錯誤，它們不是以逗號分隔。 引號字元的識別項驅動程式專屬作業，而且會擷取使用中的 SQL_IDENTIFIER_QUOTE_CHAR 選項**SQLGetInfo**。 使用 SQL_SPECIAL_CHARACTERS 和 SQL_KEYWORDS 選項中擷取的關鍵字和特殊字元的清單**SQLGetInfo**。  
  
 為了安全起見，互通的應用程式通常加上引號以外的虛擬資料行，例如 ROWID 資料行，在 Oracle 中的所有識別項。 **SQLSpecialColumns**傳回一份虛擬資料行。 此外，如果有物件名稱中特殊字元出現的位置的特定應用程式的限制，最好是互通的應用程式，不必在這些位置中使用特殊字元。
