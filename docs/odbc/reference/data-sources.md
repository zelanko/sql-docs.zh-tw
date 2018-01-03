---
title: "資料來源 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data sources [ODBC]
- data sources [ODBC], about data sources
ms.assetid: 4ae44fa2-0b9b-4e19-ab45-c1dc93b68406
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.openlocfilehash: 84c415fd10a757cebfc365759d7fb038f9630ec4
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="data-sources"></a>資料來源
A*資料來源*是資料的來源。 它可以是檔案時，DBMS 或甚至即時資料摘要上特定資料庫。 資料可能會位於與程式，相同的電腦或網路上的某個地方的另一部電腦上。 例如，資料來源可能是 OS/2® 作業系統，透過 Novell® Netware; 上執行 Oracle DBMS透過閘道; 存取 IBM DB2 DBMS伺服器目錄中; Xbase 檔案的集合或本機的 Microsoft® Access 資料庫檔案。  
  
 資料來源的目的是要收集的所有技術存取資料所需的資訊 — 驅動程式名稱、 網路位址、 網路軟體等等，在單一放置和隱藏使用者。 使用者應該能夠查看清單，其中包含薪資、 清查和人員、 從清單中，選擇薪資和具有連接到薪資資料，而不需知道薪資資料所在的位置，或是應用程式如何到達它的應用程式。  
  
 詞彙*資料來源*不應與類似的詞彙混淆。 在此手冊， *DBMS*或*資料庫*是指資料庫程式或引擎。 進一步區分*桌面資料庫，*設計，可在個人電腦上執行以及通常缺少以完整 SQL 交易支援和*server 資料庫*設計在用戶端執行 /伺服器狀況下，以獨立的資料庫引擎和豐富的 SQL 以及交易支援特徵。 *資料庫*也是指特定集合的資料，例如 SQL Server 上的 Xbase 檔案目錄或資料庫中的集合。 它通常相當於一詞*類別目錄，*此手冊或一詞在其他地方使用*限定詞*ODBC 較舊版本中。  
  
 此章節包含下列主題。  
  
-   [資料來源的類型](../../odbc/reference/types-of-data-sources.md)  
  
-   [使用資料來源](../../odbc/reference/using-data-sources.md)  
  
-   [資料來源範例](../../odbc/reference/data-source-example.md)
