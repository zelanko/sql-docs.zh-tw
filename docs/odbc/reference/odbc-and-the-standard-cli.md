---
title: "ODBC 和標準 CLI |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC [ODBC], CLI
- CLI [ODBC]
- CLI [ODBC], about CLI
- call-level interface [ODBC]
- call-level interface [ODBC], about call-level interface
ms.assetid: 79b9c268-16ac-4b80-b451-f9dcd8c02ca4
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3dd0120602e6f6fe82022aff75bb7d8157dd5bd8
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="odbc-and-the-standard-cli"></a>ODBC 和標準 CLI
ODBC 對齊下列規格和處理的呼叫層級介面 (CLI) 標準。 （ODBC 功能是每個這些標準的超集）。  
  
-   Open Group CAE 規格 」 資料管理： SQL 呼叫層級介面 (CLI) 」  
  
-   ISO/IEC 9075-3:1995 (E) 呼叫層級介面 (SQL/CLI)  
  
 由於此對齊方式，在下列條件成立：  
  
-   若要開啟 群組和 ISO CLI 規格所撰寫的應用程式將會使用 ODBC 3。*x*驅動程式或標準相容的驅動程式編譯時與 ODBC 3。*x*標頭檔，並連結到 ODBC 3。*x*程式庫，以及當它所獲得的存取權的驅動程式透過 ODBC 3。*x*驅動程式管理員。  
  
-   寫入的 Open Group 和 ISO CLI 規格的驅動程式將會使用 ODBC 3*.x*應用程式或標準相容的應用程式編譯時與 ODBC 3*.x*標頭檔和連結ODBC 3*.x*文件庫和應用程式時取得存取權的驅動程式透過 ODBC 3*.x*驅動程式管理員。 (如需詳細資訊，請參閱[符合標準的應用程式和驅動程式](../../odbc/reference/develop-app/standards-compliant-applications-and-drivers.md)。  
  
 核心介面的一致性層級包含 ISO CLI 中的所有功能以及在開啟 CLI 中群組的所有 nonoptional 功能。 開啟群組 CLI 個選擇性功能會出現在較高的介面一致性層級。 因為所有的 ODBC 3。*x*驅動程式所需的核心介面的一致性層級中支援的功能，下列條件成立：  
  
-   ODBC 3。*x*驅動程式會支援符合標準的應用程式所使用的所有功能。  
  
-   ODBC 3。*x*使用 ISO CLI 中的功能和開啟群組 CLI nonoptional 功能的應用程式將會使用任何標準相容的驅動程式。  
  
 除了 ISO/IEC 與開啟群組 CLI 標準中所包含的呼叫層級介面規格，ODBC 會實作下列功能。 （這其中部分功能在於 ODBC 3 之前的 ODBC 版本中。*x*。)  
  
-   多重資料列會擷取單一函式呼叫  
  
-   繫結至參數陣列  
  
-   包含書籤、 可變長度的書籤，並大量擷取的書籤支援更新和刪除的不連續的資料列的書籤作業  
  
-   資料列取向的繫結  
  
-   繫結位移  
  
-   支援批次的 SQL 陳述式、 預存程序或以透過執行 SQL 陳述式的序列**SQLExecute**或**SQLExecDirect**  
  
-   精確或大約的資料指標的資料列計數  
  
-   定位更新和刪除作業和批次的更新和刪除函式呼叫 (**SQLSetPos**)  
  
-   資訊結構描述，而不需要支援資訊結構描述檢視中擷取資訊的目錄函數  
  
-   外部聯結、 純量函數、 日期時間常值、 間隔常值和預存程序的逸出序列  
  
-   字碼頁轉譯程式庫  
  
-   驅動程式的 ANSI 一致性層級以及 SQL 支援報告  
  
-   視實作參數描述項的自動母體擴展  
  
-   增強的診斷和資料列和參數狀態陣列  
  
-   日期時間、 間隔、 數字/小數和 64 位元整數的應用程式緩衝區類型  
  
-   非同步執行  
  
-   預存程序支援，包括逸出序列，輸出參數繫結機制，以及目錄函數  
  
-   連接增強功能包括支援的連接屬性和瀏覽屬性
