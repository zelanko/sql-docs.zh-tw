---
title: 識別符參數 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- identifier arguments [ODBC]
- catalog functions [ODBC], arguments
- arguments in catalog functions [ODBC], identifier
ms.assetid: b9de003f-cb49-4dec-b528-14a5b8ff12bd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6831eab30daebe37baecebe3ed7053537d7de8f8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300158"
---
# <a name="identifier-arguments"></a>識別碼引數
如果引用識別符參數中的字串,驅動程式將刪除前導和尾隨空格,並從字面上處理引號中的字串。 如果未引用字串,驅動程式將刪除尾隨空格並將字串摺疊到大寫。 將標識符參數設置為空指標將返回SQL_ERROR和 SQLSTATE HY009(無效使用空指標),除非參數是目錄名稱且不支援目錄。  
  
 如果將SQL_ATTR_METADATA_ID語句屬性設置為SQL_TRUE,則這些參數將被視為標識符參數。 在這種情況下,下劃線 (*) 和百分比符號 (%)將被視為實際字元,而不是搜索模式字元。 如果此屬性設置為SQL_FALSE,則這些參數將被視為普通參數或模式參數,具體取決於參數。  
  
 儘管包含特殊字元的標識符必須在 SQL 語句中引用,但在作為目錄函數參數傳遞時不得引用這些標識符,因為傳遞給目錄函數的報價字元是字面上解釋的。 例如,假設標識符引號字元(特定於驅動程式並通過**SQLGetInfo**返回)是雙引號 ()。 對**SQLTables**的第一個調用返回一個包含有關應付帳款表的資訊的結果集,而第二個調用返回有關"應付帳款"表的資訊,這可能不是預期。  
  
```  
SQLTables(hstmt1, NULL, 0, NULL, 0, "Accounts Payable", SQL_NTS, NULL, 0);  
SQLTables(hstmt2, NULL, 0, NULL, 0, "\"Accounts Payable\"", SQL_NTS, NULL, 0);  
```  
  
 引用的識別碼用於區分真實列名和同名的偽列,如 Oracle 中的 ROWID。 如果在目錄函數的參數中傳遞了"ROWID",則該函數將使用ROWID偽列(如果存在)。 如果偽列不存在,則函數將使用"ROWID"列。 如果在目錄函數的參數中傳遞 ROWID,則該函數將使用 ROWID 列。  
  
 有關參考識別碼的詳細資訊,請參考[識別碼](../../../odbc/reference/develop-app/quoted-identifiers.md)。
