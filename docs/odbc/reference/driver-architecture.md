---
title: 驅動程式架構 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC architecture [ODBC], drivers
- drivers [ODBC], architecture
ms.assetid: c5003413-0cc1-4f41-b877-a64e2f5ab118
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a8e49b89d233880652f4b19879ff8e658bc4abe1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47628396"
---
# <a name="driver-architecture"></a>驅動程式架構
驅動程式架構分為兩種類別，根據哪個軟體程序的 SQL 陳述式：  
  
-   **檔案為基礎的驅動程式**驅動程式會直接存取實體的資料。 在此情況下，驅動程式可同時作為驅動程式和資料來源;也就是說，它會處理呼叫 ODBC 和 SQL 陳述式。 比方說，dBASE 驅動程式是檔案為基礎的驅動程式，因為 dBASE 不提供獨立的資料庫引擎驅動程式可以使用。 請務必請注意，檔案為基礎的驅動程式的開發人員必須撰寫自己的資料庫引擎。  
  
-   **以 DBMS 為基礎的驅動程式**驅動程式會透過個別的資料庫引擎存取的實體資料。 在此情況下，驅動程式處理僅 ODBC 呼叫;它會傳遞 SQL 陳述式給資料庫引擎進行處理。 例如，Oracle 驅動程式是以 DBMS 為基礎的驅動程式，因為 Oracle 驅動程式會使用獨立的資料庫引擎。 Database engine 所在的位置不是那麼重要。 它可以存在於此驅動程式與相同的電腦或不同的機器上網路，甚至可能是透過閘道存取。  
  
 驅動程式架構的驅動程式寫入器; 通常只有有趣的是也就是驅動程式架構通常會讓應用程式並沒有差別。 不過，不論應用程式可以使用的 DBMS 特定 SQL，可能會影響架構。 例如，Microsoft Access 提供獨立的資料庫引擎。 如果 Microsoft Access 驅動程式是以 DBMS 為基礎，透過此引擎存取的資料，應用程式可以將 Microsoft Access – SQL 陳述式傳遞給引擎進行處理。  
  
 不過，如果檔案為基礎的驅動程式 — 也就是它包含一個專屬的引擎，會直接存取 Microsoft® Access.mdb 檔 — Microsoft 存取特定 SQL 陳述式傳遞至引擎的任何嘗試都可能會造成語法錯誤。 原因是有可能實作只 ODBC SQL 專屬的引擎。  
  
 此章節包含下列主題。  
  
-   [以檔案為基礎的驅動程式](../../odbc/reference/file-based-drivers.md)  
  
-   [以 DBMS 為基礎的驅動程式](../../odbc/reference/dbms-based-drivers.md)  
  
-   [網路範例](../../odbc/reference/network-example.md)  
  
-   [其他驅動程式架構](../../odbc/reference/other-driver-architectures.md)
