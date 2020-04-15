---
title: 標識符案例 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- identifiers [ODBC], case
- interoperability of SQL statements [ODBC], identifier case
ms.assetid: ee8a31aa-389d-4dd1-bfa9-547f6b50bc70
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 940d96ece6b2c344fa02e0daadd6248270f4d19e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300148"
---
# <a name="identifier-case"></a>識別碼大小寫
在 SQL 語句和目錄函數參數中,標識符和引號識別符可以是區分大小寫或不,應用程式可以通過使用SQL_IDENTIFIER_CASE和SQL_QUOTED_IDENTIFIER_CASE選項調用**SQLGetInfo**來確定。  
  
 每個選項都有四個可能的返回值:一個表示標識符或引號標識符大小寫是敏感的,三個表示它不敏感。 不區分大小寫的三個值進一步描述了標識符存儲在系統目錄中的情況。 標識碼在系統目錄中的儲存方式僅與顯示目的相關,例如當應用程式顯示目錄函數的結果時;當應用程式顯示目錄函數的結果時,如何將識別碼儲存在系統目錄中。它不更改標識符的區分大小寫。
