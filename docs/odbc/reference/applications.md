---
title: 應用程式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dc655740701822d8c6ff9595327b906ee9a67026
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62734994"
---
# <a name="applications"></a>應用程式
*應用程式*是呼叫 ODBC API 來存取資料的程式。 雖然可能會有許多種應用程式，大部分會分成三個類別，做為本指南的範例。  
  
-   **一般應用程式**這些也稱為壓縮包裝的應用程式或市售的應用程式。 一般應用程式被設計用於搭配各種不同的 Dbms。 範例包括試算表或統計資料封裝會使用 ODBC 來匯入資料以供進一步分析，然後使用 ODBC 來從資料庫取得郵寄清單文書處理器。  
  
     一般應用程式的重要子類別目錄是應用程式開發環境，例如 PowerBuilder 或 Microsoft® Visual Basic®。 雖然這些環境所建構的應用程式可能只會使用單一的 DBMS，環境本身必須使用多個 Dbms。  
  
     項目所有的泛型應用程式的共通是它們是在 Dbms 之間高度互通，而且他們需要使用 ODBC 相當一般的方式。 如需有關互通性的詳細資訊，請參閱[選擇 層級的互通性](../../odbc/reference/develop-app/choosing-a-level-of-interoperability.md)。  
  
-   **垂直應用程式**垂直應用程式執行單一工作，例如訂單項目或追蹤製造資料類型，並使用受控制的應用程式開發人員的資料庫結構描述。 對特定的客戶，應用程式會使用單一的 DBMS。 例如，小型企業可能使用應用程式 dBase，而大型企業可能會使用它與 Oracle。  
  
     雖然它可能會繫結至有限數目的 Dbms 提供類似功能的應用程式使用 ODBC 應用程式不會繫結至任何一個的 DBMS，以此方式。 因此，應用程式開發人員可以銷售分開 DBMS 應用程式。 開發，但有時候修改成包含 noninteroperable 的程式碼，客戶選擇 DBMS 後，垂直的應用程式是具互通性。  
  
-   **自訂應用程式**自訂應用程式用來在一家公司中執行特定工作。 比方說，某大公司中的應用程式可能從數個分區 （其中每個使用不同的 DBMS） 中收集銷售資料，並建立單一的報表。 因為它是通用介面，讓程式設計人員不必了解多個介面，則會使用 ODBC。 這類應用程式中通常不具互通性，並寫入至特定的 Dbms 和驅動程式。  
  
 數項工作通用於所有的應用程式，無論他們如何使用 ODBC。 它們會結合起來，主要是定義任何 ODBC 應用程式的流程。 工作包括：  
  
-   選取資料來源，並連接到它。  
  
-   正在提交 SQL 陳述式執行。  
  
-   （如果有的話），請擷取結果。  
  
-   處理錯誤。  
  
-   認可或回復交易封入的 SQL 陳述式。  
  
-   正在中斷連接資料來源。  
  
 因為大部分的資料存取工作是使用 SQL，應用程式使用 ODBC 的主要工作是提交 SQL 陳述式並擷取這些陳述式所產生的結果 （如果有的話）。 其他應用程式使用 ODBC 的工作包括判斷和調整驅動程式功能，並瀏覽資料庫目錄。
