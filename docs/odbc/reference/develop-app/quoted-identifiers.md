---
title: 引言的識別碼 :微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81282001"
---
# <a name="quoted-identifiers"></a>引號識別碼
在 SQL 語句中,包含特殊字元或匹配關鍵字的標識符必須包含在*識別元報價字元*中;這些字元中包含的標識符稱為*引號識別碼*(也稱為 SQL-92 中的*分隔識別碼*)。 例如,應付帳款識別碼在以下**SELECT**語句中引用:  
  
```  
SELECT * FROM "Accounts Payable"  
```  
  
 引用標識符的原因是使語句可解析。 例如,如果上一個語句中未引用應付帳款,則解析器將假定有兩個表,即"應付帳款"和"應付帳款",並返回一個語法錯誤,即它們未用逗號分隔。 標識元報價字元特定於驅動程式,並且使用**SQLGetInfo**中的SQL_IDENTIFIER_QUOTE_CHAR選項進行檢索。 使用**SQLGetInfo**中SQL_SPECIAL_CHARACTERS和SQL_KEYWORDS選項檢索特殊字元和關鍵字的清單。  
  
 為了安全起見,可互通的應用程式通常引用除偽列以外的所有標識符,例如 Oracle 中的 ROWID 列。 **SQL 特殊列**傳回偽列清單。 此外,如果存在特殊字元在物件名稱中顯示的位置,則最好對可互通的應用程式在這些位置不使用特殊字元。
