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
manager: craigg
ms.openlocfilehash: 5485da176b9bd4aa7afca7afa088e6932d6f0d58
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47814098"
---
# <a name="odbc-and-the-standard-cli"></a>ODBC 和標準 CLI
ODBC 與下列規格和處理使用呼叫層級介面 (CLI) 中的標準。 （ODBC 功能是每個這些標準的超集）。  
  
-   開啟 群組 CAE 規格 「 資料管理： SQL 呼叫層級介面 (CLI) 」  
  
-   ISO/IEC 9075-3:1995 (E) 呼叫層級介面 (SQL/CLI)  
  
 由於這種對齊方式，在下列情況成立：  
  
-   若要開啟 群組和 ISO CLI 規格所撰寫的應用程式將會使用 ODBC 3。*x*驅動程式或符合標準的驅動程式時進行編譯 ODBC 3。*x*標頭檔，並與 ODBC 3 連結。*x*程式庫，以及當它取得的存取權的驅動程式透過 ODBC 3 時。*x*驅動程式管理員。  
  
-   寫入的 Open Group 和 ISO CLI 規格的驅動程式會使用 ODBC 3 *.x*應用程式或與標準相容的應用程式時它會使用 ODBC 3 編譯 *.x*標頭檔，並連結ODBC 3 *.x*程式庫，並當應用程式會取得存取權的驅動程式透過 ODBC 3 *.x*驅動程式管理員。 (如需詳細資訊，請參閱 <<c0> [ 標準相容的應用程式和驅動程式](../../odbc/reference/develop-app/standards-compliant-applications-and-drivers.md)。  
  
 核心介面一致性層級包含 ISO CLI 中的所有功能，開啟群組 CLI 中的所有 nonoptional 功能。 開啟群組 CLI 的選用功能會出現在較高的介面一致性層級。 因為所有的 ODBC 3。*x*驅動程式所需的核心介面一致性層級中支援的功能，下列條件成立：  
  
-   ODBC 3。*x*驅動程式將支援符合標準的應用程式所使用的所有功能。  
  
-   ODBC 3。*x*使用 ISO CLI 中的功能和開啟群組 CLI nonoptional 功能的應用程式會使用任何標準相容的驅動程式。  
  
 除了呼叫層級介面規格 ISO/IEC 與開啟群組 CLI 標準中所包含的情況下，ODBC 會實作下列功能。 （其中某些功能已在 ODBC 3 之前的 ODBC 版本。*x*。)  
  
-   多重資料列會擷取單一函式呼叫  
  
-   繫結至參數陣列  
  
-   書籤的支援，包括擷取書籤、 可變長度的書籤，並大量更新和刪除不連續的資料列的書籤作業  
  
-   資料列取向的繫結  
  
-   繫結位移  
  
-   支援的 SQL 陳述式、 預存程序或以一連串的 SQL 陳述式，透過執行批次**SQLExecute**或**SQLExecDirect**  
  
-   精確或大約的資料指標的資料列計數  
  
-   定位更新和刪除作業和批次的更新和刪除函式呼叫 (**SQLSetPos**)  
  
-   目錄資訊結構描述，而不需要支援資訊結構描述檢視中擷取資訊的函式  
  
-   外部聯結 」、 「 純量函式 」、 「 日期時間常值 」、 「 間隔常值和 「 預存程序的逸出序列  
  
-   字碼頁轉譯程式庫  
  
-   驅動程式的 ANSI 合規性層級，以及 SQL 支援報告  
  
-   視實作參數描述項的自動母體擴展  
  
-   增強的診斷和資料列和參數狀態陣列  
  
-   日期時間間隔，數字/與 64 位元整數的應用程式緩衝區類型  
  
-   非同步執行  
  
-   預存程序支援，包括逸出序列，輸出參數繫結機制，以及目錄函式  
  
-   其中包括連接屬性和屬性瀏覽支援的連線增強功能
