---
title: "驅動程式架構 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC architecture [ODBC], drivers
- drivers [ODBC], architecture
ms.assetid: c5003413-0cc1-4f41-b877-a64e2f5ab118
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a74f6e1b212f570ba9aa47a09310b63b13ee0e42
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="driver-architecture"></a>驅動程式架構
驅動程式架構分為兩種類別，根據哪個軟體處理序的 SQL 陳述式：  
  
-   **以檔案為基礎的驅動程式**驅動程式可直接存取實體的資料。 在此情況下，驅動程式作為驅動程式和資料來源;也就是說，它會處理呼叫 ODBC 和 SQL 陳述式。 例如，dBASE 驅動程式是以檔案為基礎的驅動程式，因為 dBASE 不提供獨立的資料庫引擎驅動程式就可以使用。 請務必注意的檔案為基礎的驅動程式的開發人員必須撰寫自己的資料庫引擎。  
  
-   **DBMS 架構驅動程式**驅動程式會透過不同的資料庫引擎來存取實體的資料。 驅動程式在此情況下處理僅 ODBC 呼叫。傳遞 SQL 陳述式至 database engine 的處理。 例如，Oracle 驅動程式是 DBMS 架構驅動程式，因為 Oracle 驅動程式會使用獨立的資料庫引擎。 Database engine 所在的位置並不重要。 它可以位於相同的驅動程式的電腦或不同的電腦上網路。即使可能透過閘道存取。  
  
 驅動程式架構的驅動程式寫入器; 通常只有有趣的是也就是說，驅動程式架構通常會造成任何差異，應用程式。 不過，架構會影響是否應用程式可以使用 DBMS 專屬 SQL。 例如，Microsoft Access 提供獨立的資料庫引擎。 如果 Microsoft Access 驅動程式是以 DBMS 為基礎，透過此引擎存取的資料 — 應用程式可以將 Microsoft Access – SQL 陳述式傳遞給引擎進行處理。  
  
 不過，如果驅動程式是以檔案為基礎-也就是它包含可直接存取 Microsoft® Access.mdb 檔案的專屬引擎 — 將 Microsoft 存取特定 SQL 陳述式傳遞給引擎的任何嘗試都可能會造成語法錯誤。 原因是有可能實作僅 ODBC SQL 專屬的引擎。  
  
 此章節包含下列主題。  
  
-   [以檔案為基礎的驅動程式](../../odbc/reference/file-based-drivers.md)  
  
-   [DBMS 架構驅動程式](../../odbc/reference/dbms-based-drivers.md)  
  
-   [網路範例](../../odbc/reference/network-example.md)  
  
-   [其他驅動程式架構](../../odbc/reference/other-driver-architectures.md)

