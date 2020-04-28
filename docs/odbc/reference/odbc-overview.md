---
title: ODBC 總覽 |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81298288"
---
# <a name="odbc-overview"></a>ODBC 概觀
開放式資料庫連接（ODBC）是廣為接受的應用程式開發介面（API），可用於資料庫存取。 它是以開放式群組的呼叫層級介面（CLI）規格，以及適用于資料庫 Api 的 ISO/IEC 為基礎，並使用結構化查詢語言 (SQL) （SQL）作為其資料庫存取語言。  
  
 ODBC 是針對最大的*互通性*所設計，也就是單一應用程式使用相同的原始程式碼存取不同的資料庫管理系統（dbms）的能力。 資料庫應用程式會呼叫 ODBC 介面中的函式，這些函數會在稱為*驅動程式*的資料庫特定模組中執行。 使用驅動程式會將應用程式與資料庫特定的呼叫隔離，方式與印表機驅動程式會從印表機特定的命令隔離文字處理程式。 因為驅動程式是在執行時間載入，所以使用者只需要加入新的驅動程式，就能存取新的 DBMS。不需要重新編譯或重新連結應用程式。  
  
 此章節包含下列主題。  
  
-   [為什麼建立 ODBC？](../../odbc/reference/why-was-odbc-created.md)  
  
-   [什麼是 ODBC？](../../odbc/reference/what-is-odbc.md)  
  
-   [ODBC 和標準 CLI](../../odbc/reference/odbc-and-the-standard-cli.md)
