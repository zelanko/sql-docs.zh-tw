---
title: "ODBC 概觀 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC [ODBC]
- ODBC [ODBC], about ODBC
ms.assetid: 233315bd-2b7f-4b20-9978-e920e1ea9a07
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 20767544a83219c6583eaf03a78e240e15e19be2
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="odbc-overview"></a>ODBC 概觀
開放式資料庫連接 (ODBC) 是資料庫存取廣為接受的應用程式開發介面 (API)。 它的 Open Group 和 ISO/IEC 從資料庫 Api 的呼叫層級介面 (CLI) 規格為基礎，並為其資料庫存取語言中使用結構化查詢語言 (SQL)。  
  
 ODBC 針對最大值*互通性*-也就是單一的應用程式存取相同的原始程式碼與不同的資料庫管理系統 (Dbms) 的能力。 資料庫應用程式呼叫函式在 ODBC 介面中，這會在呼叫的特定資料庫的模組中實作*驅動程式*。 使用驅動程式會從資料庫特有呼叫的應用程式隔離的印表機驅動程式隔離印表機特定命令的文字處理程式的方式相同。 因為已在執行階段載入驅動程式，使用者只需要加入新的驅動程式來存取新的 DBMS;您不需要重新編譯或重新連結應用程式。  
  
 此章節包含下列主題。  
  
-   [為什麼建立 ODBC？](../../odbc/reference/why-was-odbc-created.md)  
  
-   [什麼是 ODBC？](../../odbc/reference/what-is-odbc.md)  
  
-   [ODBC 和標準 CLI](../../odbc/reference/odbc-and-the-standard-cli.md)

