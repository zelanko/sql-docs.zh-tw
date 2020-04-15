---
title: ODBC 概述 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC]
- ODBC [ODBC], about ODBC
ms.assetid: 233315bd-2b7f-4b20-9978-e920e1ea9a07
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0a0515a882cd7d1c97a60e9262942bd7c397b0b2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298288"
---
# <a name="odbc-overview"></a>ODBC 概觀
開放資料庫連接 (ODBC) 是一個被廣泛接受的應用程式程式設計介面 (API) 用於資料庫訪問。 它基於開放組和 ISO/IEC 的資料庫 API 的呼叫級介面 (CLI) 規範,並使用結構化查詢語言 (SQL) 作為其資料庫訪問語言。  
  
 ODBC 旨在實現最大的*互通性*,即單個應用程式能夠使用相同的原始碼存取不同的資料庫管理系統 (DBMS)。 資料庫應用程式調用 ODBC 介面中的函數,這些函數在稱為*驅動程式*的特定於資料庫的模組中實現。 使用驅動程式將應用程式與特定於資料庫的調用隔離開來,就像印表機驅動程式將字處理程式與特定於印表機的命令隔離一樣。 由於驅動程式在運行時載入,因此使用者只需添加新驅動程式才能存取新的 DBMS;因此,使用者只需添加新驅動程式,使用者就只需添加新驅動程式,使用者就只需添加新的 DBMS。無需重新編譯或重新連結應用程式。  
  
 此章節包含下列主題。  
  
-   [為什麼建立 ODBC？](../../odbc/reference/why-was-odbc-created.md)  
  
-   [什麼是 ODBC？](../../odbc/reference/what-is-odbc.md)  
  
-   [ODBC 和標準 CLI](../../odbc/reference/odbc-and-the-standard-cli.md)
