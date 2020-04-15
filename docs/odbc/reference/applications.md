---
title: 應用 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306549"
---
# <a name="applications"></a>應用程式
*應用程式*是調用 ODBC API 存取資料的程式。 儘管許多類型的應用程式是可能的,但大多數分為三類,這些類別在整個本指南中用作示例。  
  
-   **通用應用程式**這些也稱為收縮包裝應用程式或現成的應用程式。 通用應用程式設計用於各種不同的 DBMS。 範例包括使用 ODBC 匯入資料進行進一步分析的電子表格或統計資訊套件,以及使用 ODBC 從資料庫獲取郵件清單的字處理器。  
  
     通用應用程式的一個重要子類別是應用程式開發環境,如 PowerBuilder 或 Microsoft®可視化基本®。 儘管使用這些環境構建的應用程式可能只與單個 DBMS 一起工作,但環境本身需要使用多個 DBMS。  
  
     所有通用應用程式都有一個共同點,它們在 DBMS 之間高度互通,並且需要以相對通用的方式使用 ODBC。 有關互通性的詳細資訊,請參閱[選擇互通性等級](../../odbc/reference/develop-app/choosing-a-level-of-interoperability.md)。  
  
-   **垂直應用**垂直應用程式執行單一類型的任務,如訂單輸入或跟蹤製造數據,並處理由應用程式開發人員控制的資料庫架構。 對於特定客戶,應用程式與單個 DBMS 一起工作。 例如,小型企業可能會將應用程式與 dBase 一起使用,而大型企業可能會將其與 Oracle 一起使用。  
  
     應用程式使用 ODBC 的方式使應用程式不綁定到任何一個 DBMS,儘管它可能與提供類似功能的有限數量的 DBMS 相關聯。 因此,應用程式開發人員可以獨立於 DBMS 銷售應用程式。 垂直應用程式在開發時可互通,但有時在客戶選擇 DBMS 後對其進行修改以包括不可互通的代碼。  
  
-   **自訂應用程式**自定義應用程式用於在單個公司中執行特定任務。 例如,大公司中的應用程式可能會從多個部門(每個部門使用不同的 DBMS)收集銷售數據,並創建單個報表。 使用 ODBC 是因為它是一個通用介面,使程式師不必學習多個介面。 此類應用程式通常不可互通,並寫入特定的 DBMS 和驅動程式。  
  
 許多任務是所有應用程式共有的,無論它們如何使用ODBC。 綜合起來,它們在很大程度上定義了任何 ODBC 應用程式的流。 工作包括:  
  
-   選擇資料來源並連接到資料來源。  
  
-   提交 SQL 語句以執行。  
  
-   檢索結果(如果有)。  
  
-   處理錯誤。  
  
-   提交或回滾包圍 SQL 語句的事務。  
  
-   與數據源斷開連接。  
  
 由於大多數數據訪問工作都使用 SQL 完成,因此應用程式使用 ODBC 的主要任務是提交 SQL 語句並檢索這些語句生成的結果(如果有)。 應用程式使用 ODBC 的其他任務包括確定和調整驅動程式功能以及流覽資料庫目錄。
