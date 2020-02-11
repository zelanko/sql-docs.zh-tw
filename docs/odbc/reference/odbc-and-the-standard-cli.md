---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5222282bce2acf49cc6a144667ddd691528b3693
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67944841"
---
# <a name="odbc-and-the-standard-cli"></a>ODBC 和標準 CLI
ODBC 會與處理呼叫層級介面（CLI）的下列規格和標準一致。 （ODBC 功能是每個標準的超集合）。  
  
-   Open Group CAE 規格 "資料管理： SQL 呼叫層級介面（CLI）"  
  
-   ISO/IEC 9075-3:1995 （E）呼叫層級介面（SQL/CLI）  
  
 由於這項調整的結果，下列條件成立：  
  
-   寫入 Open 群組和 ISO CLI 規格的應用程式，會*使用 odbc 3.x 驅動程式*或符合標準的驅動程式（當它使用 odbc 3.x 標頭檔進行編譯並*與 odbc 3.x* *程式庫一起*使用時），以及當它透過 odbc *3.x 驅動程式*管理員取得驅動程式的存取權時。  
  
-   寫入開放式群組和 ISO CLI 規格的驅動程式，會*使用 odbc 3.x 應用程式*或符合標準的應用程式，當它是使用 odbc 3.x 標頭檔進行編譯並*與 odbc 3.x* *程式庫相*連結時，以及當應用程式透過 odbc *3.x 驅動程式*管理員取得驅動程式的存取權時。 （如需詳細資訊，請參閱[符合標準的應用程式和驅動](../../odbc/reference/develop-app/standards-compliant-applications-and-drivers.md)程式。  
  
 核心介面一致性層級包含 ISO CLI 中的所有功能，以及開放式群組 CLI 中的所有 nonoptional 功能。 開放式群組 CLI 的選擇性功能會出現在更高的介面一致性層級中。 由於所有的*ODBC 3.x*驅動程式都必須支援核心介面一致性層級的功能，因此下列條件成立：  
  
-   *ODBC 3.x 驅動程式將*支援符合標準的應用程式所使用的所有功能。  
  
-   僅使用 ISO CLI 中的功能和 Open Group CLI 的 nonoptional 功能的 ODBC 3.x 應用程式，將適用于任何符合標準的*驅動程式。*  
  
 除了 ISO/IEC 和 Open Group CLI 標準中包含的呼叫層級介面規格之外，ODBC 還會執行下列功能。 （其中有一些功能存在於 ODBC 3.x 之前*的 odbc 版本中）。*  
  
-   多資料列由單一函式呼叫提取  
  
-   系結至參數陣列  
  
-   書簽支援，包括依書簽提取、可變長度的書簽，以及在不連續資料列上進行書簽作業的大量更新和刪除  
  
-   資料列取向的繫結  
  
-   系結位移  
  
-   支援 SQL 語句的批次，不論是在預存程式中，或是透過**SQLExecute**或**SQLEXECDIRECT**執行的 sql 語句序列。  
  
-   精確或近似的資料指標資料列計數  
  
-   以函式呼叫（**SQLSetPos**）定點更新和刪除作業，以及批次更新和刪除  
  
-   從資訊架構解壓縮資訊，而不需要支援資訊架構視圖的目錄函式  
  
-   外部聯結、純量函數、datetime 常值、間隔常值和預存程式的轉義順序  
  
-   字碼頁轉譯程式庫  
  
-   報告驅動程式的 ANSI 一致性層級和 SQL 支援  
  
-   視需要自動擴展的執行參數描述項  
  
-   增強的診斷和資料列和參數狀態陣列  
  
-   Datetime、interval、numeric/decimal 和64位整數應用程式緩衝區類型  
  
-   非同步執行  
  
-   預存程式支援，包括逸出序列、輸出參數系結機制和目錄函數  
  
-   連接增強功能，包括支援連接屬性和屬性流覽
