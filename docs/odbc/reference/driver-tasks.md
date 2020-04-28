---
title: 驅動程式工作 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC architecture [ODBC], drivers
- drivers [ODBC], tasks
ms.assetid: 184c795a-c2e8-4d20-9902-12e60b2f0e45
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1b30df63a3c955d2ed074ab13649ea55c21a6da7
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81294198"
---
# <a name="driver-tasks"></a>驅動程式工作
驅動程式執行的特定工作包括：  
  
-   連接到資料來源並中斷其連線。  
  
-   檢查驅動程式管理員未檢查的函數錯誤。  
  
-   起始交易;這對應用程式而言是透明的。  
  
-   正在將 SQL 語句提交至資料來源以供執行。 驅動程式必須將 ODBC SQL 修改為 DBMS 特定的 SQL;這通常僅限於以 DBMS 特定的 SQL 取代 ODBC 所定義的 escape 子句。  
  
-   將資料傳送至資料來源，並從中抓取資料，包括轉換應用程式所指定的資料類型。  
  
-   將 DBMS 特有的錯誤對應至 ODBC SQLSTATEs。
