---
description: 應用程式
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
ms.openlocfilehash: dc811b075eb698e5127fc321406bf906012c6d12
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88386134"
---
# <a name="applications"></a>應用程式
*應用程式*是呼叫 ODBC API 來存取資料的程式。 雖然可能有許多類型的應用程式，但大多分為三種類別，在本指南中是用來做為範例。  
  
-   **一般應用程式** 這些也稱為壓縮包裝應用程式或現成的應用程式。 一般應用程式是設計來搭配各種不同的 Dbms。 範例包括試算表或統計資料封裝，該封裝會使用 ODBC 匯入資料以進行進一步的分析，以及使用 ODBC 從資料庫取得郵寄清單的字處理器。  
  
     一般應用程式的重要子類別是應用程式開發環境，例如 PowerBuilder 或 Microsoft® Visual Basic®。 雖然使用這些環境所建立的應用程式可能只適用于單一 DBMS，但是環境本身也需要使用多個 Dbms。  
  
     所有的一般應用程式都有很常見的情況，就是它們在 Dbms 之間具有極大的互通性，而且需要以相當一般的方式使用 ODBC。 如需互通性的詳細資訊，請參閱 [選擇互通性層級](../../odbc/reference/develop-app/choosing-a-level-of-interoperability.md)。  
  
-   **垂直應用程式** 垂直應用程式會執行單一類型的工作，例如訂單輸入或追蹤製造資料，並使用由應用程式開發人員控制的資料庫架構。 針對特定的客戶，應用程式可搭配單一 DBMS 運作。 例如，小型企業可能會將應用程式與 dBase 搭配使用，而大型企業可能會將它與 Oracle 搭配使用。  
  
     應用程式會以應用程式未系結至任何一個 DBMS 的方式使用 ODBC，不過它可能會系結至提供類似功能的有限 Dbms 數目。 因此，應用程式開發人員可以從 DBMS 獨立銷售應用程式。 垂直應用程式在開發時可互通，但有時會在客戶選擇 DBMS 之後修改，以包含 noninteroperable 程式碼。  
  
-   **自訂應用程式** 自訂應用程式是用來在單一公司中執行特定工作。 例如，大型公司中的應用程式可能會從數個部門收集銷售資料， (各自使用不同的 DBMS) 並建立單一報表。 ODBC 是使用的，因為它是一個通用介面，可讓程式設計人員不必學習多個介面。 這類應用程式通常無法互通，並會寫入特定的 Dbms 和驅動程式。  
  
 無論應用程式使用 ODBC 的方式為何，都可以使用許多工具。 它們一起建立，主要是用來定義任何 ODBC 應用程式的流程。 這些工作包括：  
  
-   選取資料來源並與其連接。  
  
-   提交要執行的 SQL 語句。  
  
-   如果有任何) ， (抓取結果。  
  
-   處理錯誤。  
  
-   認可或回復包含 SQL 語句的交易。  
  
-   中斷與資料來源的連接。  
  
 由於大部分的資料存取都是使用 SQL 來完成，因此應用程式使用 ODBC 的主要工作就是提交 SQL 語句，並取得結果 (如果這些語句所產生的任何) 。 應用程式使用 ODBC 的其他工作包括判斷和調整驅動程式功能，以及流覽資料庫目錄。
