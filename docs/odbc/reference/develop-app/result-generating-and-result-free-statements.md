---
description: 會產生結果和不會產生結果的陳述式
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 31484578a544bb6f2cf3f8e37ffbac4674a7f055
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429110"
---
# <a name="result-generating-and-result-free-statements"></a>會產生結果和不會產生結果的陳述式
SQL 語句可以鬆散分為下列五個類別：  
  
-   **結果集-產生語句** 這些是產生結果集的 SQL 語句。 例如， **SELECT** 語句。  
  
-   資料**列計數-產生語句**這些是會產生受影響資料列計數的 SQL 語句。 例如， **UPDATE** 或 **DELETE** 語句。  
  
-   **資料定義語言 (DDL) 語句** 這些是修改資料庫結構的 SQL 語句。 例如， **CREATE TABLE** 或 **DROP INDEX**。  
  
-   **內容變更語句** 這些是變更資料庫內容的 SQL 語句。 例如，SQL Server 中的 **USE** 和 **SET** 語句。  
  
-   系統**管理語句**這些是用於資料庫中管理用途的 SQL 語句。 例如， **GRANT** 和 **REVOKE**。  
  
 前兩個類別中的 SQL 語句統稱為 *產生產生的語句*。 後三個類別中的 SQL 語句統稱為 *無結果語句*。 ODBC 會定義批次的語義，這些批次只包含產生結果的語句。 這些語義有很大的差異，因此是資料來源特有的。 例如，SQL Server 驅動程式不支援卸載物件，然後在相同的批次中參考或重新建立相同的物件。 因此，此手冊中使用的「 *批次* 」（batch）只是指產生結果的語句批次。
