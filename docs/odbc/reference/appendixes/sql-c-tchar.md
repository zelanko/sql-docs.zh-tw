---
title: "SQL_C_TCHAR |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- sql_c_tchar [ODBC]
- pseudo-type identifiers [ODBC], SQL_C_TCHAR
- data types [ODBC], pseudo-type identifiers
ms.assetid: 9e27c8bd-ee15-4ce9-b70a-34cf1bf16f4c
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 63c23a242b7acd7dd3cf10acb3f60dea980cd398
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="sqlctchar"></a>SQL_C_TCHAR
SQL_C_TCHAR 類型識別碼無法實際識別的資料類型。它是存在於標頭檔的 Unicode 轉換巨集。 取代為 SQL_C_CHAR 或 SQL_C_WCHAR 根據 UNICODE 設定**#define**。 它可用於傳送的字元資料就會編譯為 ANSI 和 Unicode 應用程式的應用程式。
