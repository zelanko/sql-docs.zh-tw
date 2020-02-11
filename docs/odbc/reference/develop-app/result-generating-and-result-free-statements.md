---
title: 結果產生和無結果的語句 |Microsoft Docs
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
ms.openlocfilehash: 55b2ff4d428f02b59883b675fde95531366f0b4d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68020598"
---
# <a name="result-generating-and-result-free-statements"></a>會產生結果和不會產生結果的陳述式
SQL 語句可能會鬆散分為下列五個類別：  
  
-   **結果集產生的語句**這些是產生結果集的 SQL 語句。 例如， **SELECT**語句。  
  
-   資料**列計數產生語句**這些是產生受影響資料列計數的 SQL 語句。 例如， **UPDATE**或**DELETE**語句。  
  
-   **資料定義語言（DDL）語句**這些是修改資料庫結構的 SQL 語句。 例如， **CREATE TABLE**或**DROP INDEX**。  
  
-   **內容變更語句**這些是變更資料庫內容的 SQL 語句。 例如，SQL Server 中的**USE**和**SET**語句。  
  
-   系統**管理語句**這些是在資料庫中用於系統管理目的的 SQL 語句。 例如， **GRANT**和**REVOKE**。  
  
 前兩個類別中的 SQL 語句統稱為*結果產生語句*。 後面三個類別中的 SQL 語句統稱為*無結果語句*。 ODBC 會定義批次的語義，其中只包含結果產生的語句。 這些語義的差異很大，因此是資料來源特有的。 例如，SQL Server 驅動程式不支援卸載物件，然後在相同的批次中參考或重新建立相同的物件。 因此，此手冊中使用的「*批次*」一詞只會參考結果產生語句的批次。
