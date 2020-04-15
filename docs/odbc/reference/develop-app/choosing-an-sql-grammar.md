---
title: 選擇 SQL 語法 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], SQL grammar
- SQL grammar [ODBC], selecting
ms.assetid: 4e0d189b-e407-47e0-92a9-f9982230dd0e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2ca9911d3c88f2f540ff1332d77a2e1ebc6a4942
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299158"
---
# <a name="choosing-an-sql-grammar"></a>選擇 SQL 文法
建構 SQL 語句時要做出的第一個決定是使用哪個語法。 除了開放組、ANSI 和 ISO 等各種標準機構提供的語法外,幾乎每個 DBMS 供應商都定義自己的語法,每個語法與標準略有不同。  
  
 [附錄 C:SQL 語法](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md),描述了所有 ODBC 驅動程式必須支援的最小 SQL 語法。 此語法是 SQL-92 條目級別的子集。 驅動程式可能支援其他語法,以符合 SQL-92 定義的中間、完整或 FIPS 127-2 過渡級別。 有關詳細資訊,請參閱附錄 C 中的[SQL 最小語法](../../../odbc/reference/appendixes/sql-minimum-grammar.md):SQL 語法和 SQL-92。  
  
 附錄 C 還定義了包含 SQL-92 語法未涵蓋的常用語言功能(如外部聯接)的標準語法的*逸出序列*。 有關詳細資訊,請參閱附錄 C 中的[ODBC 轉義序列](../../../odbc/reference/appendixes/odbc-escape-sequences.md):SQL 語法和[轉義序列](../../../odbc/reference/develop-app/escape-sequences.md),請參閱本節後面的。  
  
 所選語法會影響驅動程序處理語句的方式。 驅動程式必須修改 SQL-92 SQL 和 ODBC 定義的轉義序列到特定於 DBMS 的 SQL。 由於大多數 SQL 語法基於一個或多個各種標準,因此大多數驅動程式很少或根本沒有工作來滿足此要求。 它通常只包括搜索由 ODBC 定義的轉義序列,並用特定於 DBMS 的語法替換它們。 當驅動程式遇到它無法識別的語法時,它假定該語法特定於 DBMS,並且在不修改數據源的情況下傳遞 SQL 語句以執行。  
  
 因此,實際上有兩種語法可供選擇:SQL-92語法(和 ODBC 轉義序列)和特定於 DBMS 的語法。 在兩者中,只有 SQL-92 語法是可互通的,因此所有可互通的應用程式都應該使用它。 不可互通的應用程式可以使用 SQL-92 語法或特定於 DBMS 的語法。 特定於 DBMS 的語法有兩個優點:它們可以利用 SQL-92 未涵蓋的任何功能,並且它們的速度略快,因為驅動程式不必修改它們。 后一個功能可以通過設置SQL_ATTR_NOSCAN語句屬性部分強制執行,該屬性阻止驅動程式搜索和替換轉義序列。  
  
 如果使用 SQL-92 語法,應用程式可以通過調用**SQLNativeSql**來發現驅動程式如何修改它。 這在調試應用程式時通常很有用。 **SQLNativeSql**接受 SQL 語句,並在驅動程式修改後返回它。 由於此函數處於 Core 介面一致性級別,因此所有驅動程式都支援此功能。
