---
title: SQL_C_TCHAR |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- sql_c_tchar [ODBC]
- pseudo-type identifiers [ODBC], SQL_C_TCHAR
- data types [ODBC], pseudo-type identifiers
ms.assetid: 9e27c8bd-ee15-4ce9-b70a-34cf1bf16f4c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 973d94b9b47371090a5f54fd3d259854ba78e9c2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304069"
---
# <a name="sql_c_tchar"></a>SQL_C_TCHAR
SQL_C_TCHAR類型標識符實際上不標識數據類型;因此,該標識符實際上不會標識數據類型。它是存在在 Unicode 轉換的標頭檔中的宏。 它替換為SQL_C_CHAR或SQL_C_WCHAR,具體取決於 UNICODE **#define**的設置。 它對於傳輸字元數據的應用程式非常有用,這些數據被編譯為 ANSI 和 Unicode 應用程式。
