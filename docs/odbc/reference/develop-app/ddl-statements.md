---
title: DDL 語句 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], DDL statements
- DDL statements [ODBC]
ms.assetid: 96ac9859-5976-4b06-ae1f-2fec3231e266
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cae06efe6dd11e651e8553fa5c1004c2fa145478
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302989"
---
# <a name="ddl-statements"></a>DDL 陳述式
數據定義語言 (DDL) 語句在 DBMS 之間差異很大。 ODBC SQL 為最常見的數據定義操作定義語句:創建和刪除表、索引和視圖;更改表;授予和撤銷特權。 所有其他 DDL 語句都是特定於數據源的。 因此,可互通的應用程式無法執行某些數據定義操作。 通常,這不是問題,因為此類操作往往高度特定於 DBMS,最好留給大多數 DBMS 附帶的專有資料庫管理軟體或驅動程式附帶的安裝程式。  
  
 數據定義中的另一個問題是數據類型名稱在 DBMS 之間差異很大。 **SQLGetTypeInfo**不是定義標準數據類型名稱,而是強制驅動程式將其轉換為特定於 DBMS 的名稱,而是為應用程式提供了一種發現特定於 DBMS 的數據類型名稱的方法。 可互通的應用程式應在 SQL 語句中使用這些名稱來創建和更改表;附錄 C[中列出的名稱:SQL 語法](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)和附錄[D:數據類型](../../../odbc/reference/appendixes/appendix-d-data-types.md)僅是範例。
