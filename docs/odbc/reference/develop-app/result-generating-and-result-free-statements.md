---
title: "結果產生和無結果的陳述式 |Microsoft 文件"
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
- result-generating statements [ODBC]
- batches [ODBC], result-generating statements
- batches [ODBC], result-free statements
- SQL statements [ODBC], batches
- result-free statements [ODBC]
ms.assetid: 2f3475d1-3999-4dd8-aba2-a6e1299c95f8
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a99ea01cbd5a00ea4aa12e4b1461ca7f1ce9afa5
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="result-generating-and-result-free-statements"></a>結果產生和無結果的陳述式
SQL 陳述式可以鬆散分為下列五個類別：  
  
-   **結果集產生的陳述式**這些是產生的結果集的 SQL 陳述式。 例如，**選取**陳述式。  
  
-   **資料列計數產生陳述式**這些是產生受影響的資料列計數的 SQL 陳述式。 例如，**更新**或**刪除**陳述式。  
  
-   **資料定義語言 (DDL) 陳述式**這些是修改資料庫結構的 SQL 陳述式。 例如， **CREATE TABLE**或**DROP INDEX**。  
  
-   **內容變更陳述式**這些是變更的內容資料庫的 SQL 陳述式。 例如，**使用**和**設定**SQL Server 中的陳述式。  
  
-   **系統管理的陳述式**這些是用來在資料庫中的系統管理目的 SQL 陳述式。 例如， **GRANT**和**撤銷**。  
  
 SQL 陳述式中的前兩個類別統稱為*結果產生的陳述式*。 SQL 陳述式，後者的三個類別統稱為*結果釋放陳述式*。 ODBC 定義的包含僅結果產生的陳述式的批次的語意。 這些語意差異非常大，因此資料來源專用。 例如，SQL Server 驅動程式不支援卸除物件再參考或重新建立相同的批次中相同的物件。 因此，一詞*批次*會用在此手冊只適用於批次結果產生的陳述式。
