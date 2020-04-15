---
title: 靜態 SQL |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- static SQL [ODBC]
- SQL [ODBC], embedded SQL
- SQL statements [ODBC], embedded SQL
- SQL statements [ODBC], static SQL
- embedded SQL [ODBC]
- SQL [ODBC], static SQL
ms.assetid: 667d92ec-fed9-4028-81d4-bb9ba867356a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 55710d8ea734cba86ae5e4daa725f75e94e65a64
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81279900"
---
# <a name="static-sql"></a>靜態 SQL
[嵌入式 SQL 範例中](../../odbc/reference/embedded-sql-example.md)顯示的嵌入式 SQL 稱為靜態 SQL。 它被稱為靜態 SQL,因為程式中的 SQL 語句是靜態的;也就是說,它們不會在每次運行程式時更改。 如上一節所述,這些語句是在編譯程式的其餘部分時編譯的。  
  
 靜態 SQL 在許多情況下工作良好,可用於可在程式設計時確定數據訪問的任何應用程式中使用。 例如,訂單輸入程式始終使用相同的語句來插入新訂單,航空公司預訂系統始終使用相同的語句將座位的狀態從可用更改為預留。 這些語句中的每一個都將通過使用宿主變數進行概括;可以在銷售訂單中插入不同的值,並可以保留不同的席位。 由於此類語句可以在程式中硬編碼,因此此類程式的優點是,在編譯時,語句只需分析、驗證和優化一次。 這會導致代碼相對快速。
