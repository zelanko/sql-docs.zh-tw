---
title: "引號識別項 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], quoted identifiers
- quoted identifiers [ODBC]
ms.assetid: 729ba55f-743b-4a04-8c39-ac0a9914211d
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 07a0c8299fc4063e72353025465309c426a3a251
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="quoted-identifiers"></a>引號的識別碼
SQL 陳述式中包含特殊字元或相符的關鍵字的識別項必須括在*識別碼引號字元*; 這類字元括住的識別項稱為*引號識別項*(也稱為*分隔識別碼*以 sql-92)。 比方說，在下列引用 Accounts Payable 識別碼**選取**陳述式：  
  
```  
SELECT * FROM "Accounts Payable"  
```  
  
 引號識別項的原因是提供可以剖析陳述式。 比方說，如果 Accounts Payable 未加引號的前一個陳述式中，剖析器會假設沒有帳戶 」 和 「 應付帳款，兩個資料表，並傳回語法錯誤，不是以逗號分隔。 引號字元的識別項是驅動程式專屬功能，並擷取中的 SQL_IDENTIFIER_QUOTE_CHAR 選項**SQLGetInfo**。 關鍵字和特殊字元的清單會擷取與 SQL_SPECIAL_CHARACTERS 和 SQL_KEYWORDS 選項中**SQLGetInfo**。  
  
 為了安全起見，互通的應用程式通常加上引號的虛擬資料行，例如在 Oracle 中 「 ROWID 資料行除外的所有識別項。 **SQLSpecialColumns**會傳回一份虛擬資料行。 此外，如果有特殊字元出現在 物件名稱的位置上的特定應用程式的限制，它是最佳的可互通的應用程式不在這些位置中使用特殊字元。
