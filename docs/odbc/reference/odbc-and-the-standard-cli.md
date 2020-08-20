---
description: ODBC 和標準 CLI
title: ODBC 和標準 CLI |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC], CLI
- CLI [ODBC]
- CLI [ODBC], about CLI
- call-level interface [ODBC]
- call-level interface [ODBC], about call-level interface
ms.assetid: 79b9c268-16ac-4b80-b451-f9dcd8c02ca4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 844ca219bf912421cf859e0fc459b78d755fe159
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487381"
---
# <a name="odbc-and-the-standard-cli"></a>ODBC 和標準 CLI
ODBC 符合下列規格和標準，可處理 (CLI) 的呼叫層級介面。  (ODBC 功能是這些標準的超集合。 )   
  
-   Open Group CAE 規格 "資料管理： SQL 呼叫層級介面 (CLI) "  
  
-   ISO/IEC 9075-3:1995 (E)  (SQL/CLI 的呼叫層級介面)   
  
 這項調整的結果如下：  
  
-   寫入 Open 群組和 ISO CLI 規格的應用程式將會 *使用 odbc 3.x 的驅動程式* 或符合標準的驅動程式（使用 odbc 3.x 標頭檔進行編譯，並連結 *到 odbc 3.x* *程式庫）* ，以及透過 odbc *3.x 驅動程式* 管理員取得驅動程式的存取權。  
  
-   寫入開放式群組和 ISO CLI 規格的驅動程式，將會使用 odbc 3.x*標頭檔編譯的 odbc* *3.x 應用程式*或符合標準的應用程式，並*與 odbc 3.x 程式庫連結*，以及當應用程式透過 odbc *3.x 驅動程式*管理員取得驅動程式的存取權時。  (需詳細資訊，請參閱 [符合標準的應用程式和驅動](../../odbc/reference/develop-app/standards-compliant-applications-and-drivers.md)程式。  
  
 核心介面一致性層級包含 ISO CLI 中的所有功能，以及 Open Group CLI 中的所有 nonoptional 功能。 Open Group CLI 的選擇性功能會出現在更高的介面一致性層級中。 由於所有的 *ODBC 3.x* 驅動程式都必須支援核心介面一致性層級中的功能，因此下列條件成立：  
  
-   *ODBC 3.x 驅動程式將*支援符合標準的應用程式所使用的所有功能。  
  
-   只有 ISO CLI 中的功能和 Open 群組 CLI 的 nonoptional 功能的 ODBC 3.x 應用程式，才能與任何符合標準的 *驅動程式搭配* 使用。  
  
 除了 ISO/IEC 和 Open Group CLI 標準中包含的呼叫層級介面規格之外，ODBC 也會執行下列功能。  (其中一些功能存在 *于 odbc 3.x 之前的 odbc 版本*中 )   
  
-   單一函式呼叫的多資料列提取  
  
-   系結至參數陣列  
  
-   書簽支援，包括依書簽提取、可變長度的書簽，以及在不連續的資料列上依書簽作業進行大量更新和刪除  
  
-   資料列取向的繫結  
  
-   系結位移  
  
-   支援 SQL 語句的批次，不論是在預存程式中，或是透過**SQLExecute**或**SQLEXECDIRECT**執行的 sql 語句順序  
  
-   精確或近似的資料指標資料列計數  
  
-   依函式呼叫定點更新和刪除作業和批次更新和刪除 (**SQLSetPos**)   
  
-   從資訊架構中解壓縮資訊的目錄函式，而不需要支援資訊架構視圖  
  
-   外部聯結、純量函數、datetime 常值、間隔常值和預存程式的 Escape 序列  
  
-   程式字碼頁轉譯程式庫  
  
-   報告驅動程式的 ANSI 一致性層級和 SQL 支援  
  
-   依需求自動擴展實作為參數描述項  
  
-   增強的診斷和資料列和參數狀態陣列  
  
-   Datetime、interval、numeric/decimal 和64位整數應用程式緩衝區類型  
  
-   非同步執行  
  
-   預存程式支援，包括 escape 序列、輸出參數系結機制和目錄函數  
  
-   連接增強功能，包括支援連接屬性和屬性流覽
