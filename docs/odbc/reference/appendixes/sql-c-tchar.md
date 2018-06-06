---
title: SQL_C_TCHAR |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- sql_c_tchar [ODBC]
- pseudo-type identifiers [ODBC], SQL_C_TCHAR
- data types [ODBC], pseudo-type identifiers
ms.assetid: 9e27c8bd-ee15-4ce9-b70a-34cf1bf16f4c
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cce7467dd03210d60fad060e25885baf0df38399
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="sqlctchar"></a>SQL_C_TCHAR
SQL_C_TCHAR 類型識別碼無法實際識別的資料類型。它是存在於標頭檔的 Unicode 轉換巨集。 取代為 SQL_C_CHAR 或 SQL_C_WCHAR 根據 UNICODE 設定 **#define**。 它可用於傳送的字元資料就會編譯為 ANSI 和 Unicode 應用程式的應用程式。
