---
title: 應用程式 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- off-the-shelf applications [ODBC]
- ODBC architecture [ODBC], applications
- shrink-wrapped applications [ODBC]
- application development [ODBC], types
- custom applications [ODBC]
- virtual applications [ODBC]
- generic applications [ODBC]
ms.assetid: 39d6461f-0d24-4b7d-a723-843ade15ad73
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3237c947052b2634ec7f6a6e2c1f9909e3845827
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="applications"></a>應用程式
*應用程式*是呼叫 ODBC API 來存取資料的程式。 雖然可能會有許多類型的應用程式，絕大部分會做為範例，本指南中的三個類別。  
  
-   **泛型應用程式**這些也稱為壓縮包裝的應用程式或現成的應用程式。 泛型應用程式專為搭配各種不同的不同 Dbms。 範例包括試算表或統計資料的封裝會利用 ODBC 來匯入資料以進一步分析，然後利用 ODBC 來從資料庫取得郵寄清單文書處理器。  
  
     泛型應用程式中的重要子類別目錄是應用程式開發環境，例如 PowerBuilder 或 Microsoft® Visual Basic®。 雖然這些環境所建構的應用程式可能只會使用單一的 DBMS，本身的環境，必須使用多個 Dbms。  
  
     哪些所有泛型應用程式必須在一般是其互通性很高 Dbms 之間，而需要較一般的方式使用 ODBC。 如需有關互通性的詳細資訊，請參閱[選擇有層級的互通性](../../odbc/reference/develop-app/choosing-a-level-of-interoperability.md)。  
  
-   **垂直應用程式**垂直應用程式執行單一工作，例如訂單項目或追蹤製造資料類型，以及使用 資料庫結構描述由應用程式的開發人員所控制。 針對特定的客戶，應用程式的運作方式與單一的 DBMS。 比方說，小型企業可能會使用應用程式與 dBase，而大型企業可能會使用它與 Oracle。  
  
     雖然可能限於有限數目的 Dbms 提供類似功能的應用程式使用 ODBC 應用程式不會繫結至任何一個 DBMS，以此方式。 因此，應用程式開發人員可以販售 DBMS 獨立於應用程式。 當他們所開發，但有時候修改成包含 noninteroperable 的程式碼，客戶選擇 DBMS 後，會互通垂直應用程式。  
  
-   **自訂應用程式**自訂應用程式用來執行特定工作，一家公司中。 例如，大型公司中的應用程式可能會蒐集 （其中每個使用不同的 DBMS） 的數個區域的銷售資料並建立單一報表。 因為它是通用介面，並且將程式設計人員需要了解多個介面，會使用 ODBC。 這類應用程式通常並不互通，而且會寫入至特定 Dbms 和驅動程式。  
  
 數項工作通用於所有應用程式，不論他們使用 ODBC 的方式。 結合起來，它們主要是定義任何 ODBC 應用程式的流程。 工作如下：  
  
-   選取資料來源，並連接到它。  
  
-   正在提交 SQL 陳述式執行。  
  
-   （如果有的話），擷取結果。  
  
-   處理錯誤。  
  
-   認可或回復交易封入的 SQL 陳述式。  
  
-   中斷連接資料來源。  
  
 因為大部分的資料存取工作是使用 SQL，應用程式使用 ODBC 的主要工作是提交 SQL 陳述式並擷取這些陳述式所產生的結果 （如果有的話）。 其他應用程式使用 ODBC 的工作包括判斷和調整驅動程式功能，並瀏覽資料庫目錄。
