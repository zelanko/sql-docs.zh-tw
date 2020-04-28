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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9184986883f64bd082ca1db472d887609d3071bd
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306549"
---
# <a name="applications"></a>應用程式
*應用程式*是呼叫 ODBC API 來存取資料的程式。 雖然有許多類型的應用程式可以使用，但大部分都屬於三種類別，這在本指南中是用來做為範例。  
  
-   **一般應用程式**這些也稱為「壓縮包裝應用程式」或「現成應用程式」。 一般應用程式是設計用來處理各種不同的 Dbms。 範例包括試算表或統計資料封裝，它會使用 ODBC 匯入資料以進行進一步的分析，以及使用 ODBC 從資料庫取得郵寄清單的字處理器。  
  
     一般應用程式的一個重要子類別是應用程式開發環境，例如 PowerBuilder 或 Microsoft® Visual Basic®。 雖然使用這些環境所建立的應用程式可能只適用于單一 DBMS，但環境本身必須使用多個 Dbms。  
  
     所有的泛型應用程式都有其共同點，它們在 Dbms 之間具有高度互通性，而且需要以相對一般的方式使用 ODBC。 如需有關互通性的詳細資訊，請參閱[選擇互通性層級](../../odbc/reference/develop-app/choosing-a-level-of-interoperability.md)。  
  
-   **垂直應用程式**垂直應用程式會執行單一類型的工作，例如訂單輸入或追蹤製造資料，並使用由應用程式開發人員所控制的資料庫架構。 針對特定客戶，應用程式會與單一 DBMS 搭配運作。 例如，小型企業可能會使用應用程式搭配 dBase，而大型企業可能會將它與 Oracle 搭配使用。  
  
     應用程式會以應用程式不會系結至任何一個 DBMS 的方式來使用 ODBC，雖然它可能會系結至提供類似功能的 Dbms 數目有限。 因此，應用程式開發人員可以在 DBMS 以外獨立銷售應用程式。 垂直應用程式在開發時可互通，但有時會在客戶選擇 DBMS 之後修改為包含 noninteroperable 的程式碼。  
  
-   **自訂應用程式**自訂應用程式是用來在單一公司中執行特定工作。 例如，大型公司中的應用程式可能會從數個部門收集銷售資料（其中每一個都使用不同的 DBMS），並建立單一報表。 使用 ODBC 是因為它是一個通用的介面，可讓程式設計人員不必學習多個介面。 這類應用程式通常無法互通，而且會寫入特定的 Dbms 和驅動程式。  
  
 所有應用程式都有許多工具，不論它們使用 ODBC 的方式為何。 兩者結合在一起，主要是定義任何 ODBC 應用程式的流程。 工作包括：  
  
-   選取資料來源並與其連接。  
  
-   提交要執行的 SQL 語句。  
  
-   正在抓取結果（如果有的話）。  
  
-   處理錯誤。  
  
-   認可或回復包含 SQL 語句的交易。  
  
-   中斷與資料來源的連線。  
  
 因為大部分的資料存取工作都是使用 SQL 來完成，所以應用程式使用 ODBC 的主要工作就是提交 SQL 語句，並抓取這些語句所產生的結果（如果有的話）。 應用程式使用 ODBC 的其他工作包括判斷和調整驅動程式功能，以及流覽資料庫目錄。
