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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2e2ed50ac3f9e914953abdd64907199a5f978af2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67915464"
---
# <a name="driver-tasks"></a>驅動程式工作
特定驅動程式所執行的工作包括：  
  
-   連接到與中斷連接資料來源。  
  
-   檢查函式不會檢查驅動程式管理員的錯誤。  
  
-   起始交易;這是向應用程式。  
  
-   正在提交至資料來源，以便執行的 SQL 陳述式。 驅動程式必須修改以 DBMS 專用 SQL; 的 ODBC SQL這通常是限制為取代具有特定 DBMS 的 SQL ODBC 所定義的逸出子句。  
  
-   將資料傳送到和從資料來源，包括轉換資料類型所指定的應用程式擷取資料。  
  
-   對應至 ODBC Sqlstate 的 DBMS 特定錯誤。
