---
title: 結果生成和無結果語句 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result-generating statements [ODBC]
- batches [ODBC], result-generating statements
- batches [ODBC], result-free statements
- SQL statements [ODBC], batches
- result-free statements [ODBC]
ms.assetid: 2f3475d1-3999-4dd8-aba2-a6e1299c95f8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fc94aabd7982fba5879519573980db03b1857ef6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300088"
---
# <a name="result-generating-and-result-free-statements"></a>會產生結果和不會產生結果的陳述式
SQL 語句可以大致分為以下五個類別:  
  
-   **結果集產生敘述**這些是生成結果集的 SQL 語句。 例如 **,SELECT**語句。  
  
-   **行計數產生敘述**這些是生成受影響行計數的 SQL 語句。 例如,**更新**或**刪除**語句。  
  
-   **資料定義語言 (DDL) 語句**這些是修改資料庫結構的 SQL 語句。 例如,**建立表**或**DROP 索引**。  
  
-   **內容變更敘述**這些是更改資料庫上下文的 SQL 語句。 例如,SQL Server 中的**USE**和**SET**語句。  
  
-   **行政聲明**這些是用於資料庫中管理目的的 SQL 語句。 例如,**請指定**與**撤銷**。  
  
 前兩個類別中的 SQL 語句統稱為*產生結果語句*。 後三個類別中的 SQL 語句統稱為*無結果語句*。 ODBC 定義只包含結果生成語句的批處理的語義。 這些語義差異很大,因此特定於數據源。 例如,SQL Server 驅動程式不支援刪除物件,然後引用或在同一批處理中重新創建同一物件。 因此,本手冊中使用的術語*批處理*僅指結果生成語句的批處理。
