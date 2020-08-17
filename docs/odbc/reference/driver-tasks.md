---
description: 驅動程式工作
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
ms.openlocfilehash: 263f591592063a45fdd5afdca4efdd75b5b915b6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88339054"
---
# <a name="driver-tasks"></a>驅動程式工作
驅動程式所執行的特定工作包括：  
  
-   連接到資料來源，並中斷與資料來源的連接。  
  
-   檢查驅動程式管理員未檢查的函數錯誤。  
  
-   正在起始交易;這對應用程式而言是透明的。  
  
-   將 SQL 語句提交到資料來源以執行。 驅動程式必須將 ODBC SQL 修改為 DBMS 特定的 SQL;這通常僅限於以 DBMS 特定的 SQL 取代 ODBC 所定義的 escape 子句。  
  
-   將資料傳送到資料來源並從中抓取資料，包括轉換應用程式所指定的資料類型。  
  
-   將 DBMS 特定的錯誤對應至 ODBC SQLSTATEs。
