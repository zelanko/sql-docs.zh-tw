---
title: ODBC 概觀 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6b064436dae6cb2f3d5f37fa02ab57a1e4a3f015
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63272935"
---
# <a name="odbc-overview"></a>ODBC 概觀
開放式資料庫連接 (ODBC) 是資料庫存取廣為接受的應用程式開發介面 (API)。 它以資料庫 Api 從 Open Group 和 ISO/IEC 的呼叫層級介面 (CLI) 規格為基礎，並使用做為其資料庫存取語言的結構化查詢語言 (SQL)。  
  
 ODBC 專為最大*互通性*-也就是單一的應用程式，以存取不同的資料庫管理系統 (Dbms) 具有相同的原始碼的能力。 資料庫應用程式呼叫 ODBC 介面，該屬性在呼叫的特定資料庫的模組實作函式*驅動程式*。 使用驅動程式會從特定資料庫呼叫的應用程式隔離印表機驅動程式隔離的印表機特定命令的文字處理程式的方式相同。 因為在執行階段載入驅動程式，使用者只具有要新增新的驅動程式來存取新的 DBMS;您不需要重新編譯或重新連結應用程式。  
  
 此章節包含下列主題。  
  
-   [為什麼建立 ODBC？](../../odbc/reference/why-was-odbc-created.md)  
  
-   [什麼是 ODBC？](../../odbc/reference/what-is-odbc.md)  
  
-   [ODBC 和標準 CLI](../../odbc/reference/odbc-and-the-standard-cli.md)
