---
title: 結果產生和無結果的陳述式 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f357576e9e7510ae581b41a50976a34981f35109
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62861518"
---
# <a name="result-generating-and-result-free-statements"></a>會產生結果和不會產生結果的陳述式
SQL 陳述式可以鬆散分為下列五個類別：  
  
-   **結果集產生的陳述式**這些是產生的結果集的 SQL 陳述式。 例如，**選取**陳述式。  
  
-   **資料列計數產生陳述式**這些是產生受影響的資料列計數的 SQL 陳述式。 例如，**更新**或是**刪除**陳述式。  
  
-   **資料定義語言 (DDL) 陳述式**這些是修改資料庫結構的 SQL 陳述式。 例如， **CREATE TABLE**或是**DROP INDEX**。  
  
-   **內容變更陳述式**這些是變更的內容資料庫的 SQL 陳述式。 例如，**使用**並**設定**SQL Server 中的陳述式。  
  
-   **管理陳述式**這些是用於系統管理資料庫中的 SQL 陳述式。 例如， **GRANT**並**撤銷**。  
  
 前兩個類別中的 SQL 陳述式通稱為*結果產生的陳述式*。 在後者的三個類別中的 SQL 陳述式通稱為*無陳述式的結果的*。 ODBC 定義的批次包含只產生結果的陳述式的語意。 這些語意大不相同，因此資料來源特有。 例如，SQL Server 驅動程式不支援卸除物件然後參考或重新建立相同的批次中相同的物件。 因此，詞彙*批次*中使用這份手冊只會參考結果產生的批次陳述式。
