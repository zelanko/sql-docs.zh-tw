---
title: 編譯嵌入式 SQL 程式 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL [ODBC], embedded SQL
- SQL statements [ODBC], embedded SQL
- compiling embedded SQL programs [ODBC]
- embedded SQL [ODBC]
ms.assetid: 9e94146a-5b80-4a01-b586-1e03ff05b9ac
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: eb801dc532009410055b67031b3e036cc6b9c3d0
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306529"
---
# <a name="compiling-an-embedded-sql-program"></a>編譯內嵌 SQL 程式
由於嵌入式 SQL 程式包含 SQL 和宿主語言語句的組合,因此無法直接將其提交到主機語言的編譯器。 相反,它是通過多步驟過程編譯的。 儘管此過程因產品而異,但所有產品的步驟大致相同。  
  
 此圖顯示了編譯嵌入式 SQL 程式所需的步驟。  
  
 ![編譯內嵌的 SQL 程式之步驟](../../odbc/reference/media/pr02.gif "pr02")  
  
 編譯嵌入式 SQL 程式涉及五個步驟:  
  
1.  嵌入的 SQL 程式將提交到 SQL 預編譯器,一個程式設計工具。 預編譯器掃描程式,查找嵌入的 SQL 語句,並處理它們。 DBMS 支援的每個程式設計語言都需要不同的預編譯器。 DBMS 產品通常為一種或多種語言提供預編譯器,包括 C、Pascal、COBOL、Fortran、Ada、PL/I 和各種彙編語言。  
  
2.  預編譯器生成兩個輸出檔。 第一個檔是源檔,它刪除了嵌入的 SQL 語句。 就其位置,預編譯器將替換對專有 DBMS 例程的調用,這些例程提供程式和 DBMS 之間的運行時連結。 通常,這些例程的名稱和調用序列僅由預編譯器和 DBMS 知道;它們不是 DBMS 的公共介面。 第二個檔案是程式中使用的所有嵌入式 SQL 語句的副本。 此文件有時稱為資料庫請求模組或 DBRM。  
  
3.  預編譯器的源文件輸出將提交到主機編程語言(如 C 或 COBOL 編譯器)的標準編譯器。 編譯器處理原始碼並生成物件代碼作為其輸出。 請注意,此步驟與 DBMS 或 SQL 無關。  
  
4.  連結器接受編譯器生成的物件模組,將它們與各種庫例程連結,並生成可執行程式。 連結到可執行程式的庫例程包括步驟 2 中描述的專有 DBMS 例程。  
  
5.  預編譯器生成的資料庫請求模組將提交到特殊的綁定實用程式。 此實用程式檢查 SQL 語句、分析、驗證和優化它們,然後為每個語句生成訪問計畫。 結果是整個程式的組合存取計畫,表示嵌入式 SQL 語句的可執行版本。 綁定實用程式將計劃存儲在資料庫中,通常為其分配將用於使用它的應用程式的名稱。 此步驟是在編譯時還是運行時執行取決於 DBMS。  
  
 請注意,用於編譯嵌入式 SQL 程式的步驟與[處理 SQL 語句](../../odbc/reference/processing-a-sql-statement.md)前面描述的步驟密切相關。 特別是,請注意,預編譯器將 SQL 語句與宿主語言代碼分開,綁定實用程式解析和驗證 SQL 語句並創建訪問計畫。 在步驟 5 在編譯時發生的 DBMS 中,處理 SQL 語句的前四個步驟發生在編譯時,而最後一個步驟(執行)發生在運行時。 這具有使查詢在此類 DBMS 中執行速度非常快的效果。
