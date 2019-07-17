---
title: 資料來源 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC]
- data sources [ODBC], about data sources
ms.assetid: 4ae44fa2-0b9b-4e19-ab45-c1dc93b68406
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 92b8ca2b8c780e48cd9f3bf815ca86e3bd27081e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68135626"
---
# <a name="data-sources"></a>資料來源
A*資料來源*是資料的來源。 它可以是檔案、 DBMS 或甚至是即時的資料摘要上特定資料庫。 資料可能位於程式，在同一部電腦或網路上的某個位置的另一部電腦上。 例如，資料來源可能 OS/2® 作業系統，存取 Novell® Netware; 上執行 Oracle DBMS透過閘道; 存取 IBM DB2 DBMS在伺服器目錄; Xbase 檔案的集合或本機的 Microsoft® Access 資料庫檔案。  
  
 資料來源的目的是收集到單一位置的所有存取的資料-驅動程式名稱、 網路位址、 網路軟體等等-所需的技術資訊，並向使用者隱藏它。 使用者應該能夠查看清單，其中包含薪資、 清查和人員、 從清單中，選擇 薪資和連接到薪資資料，無須了解在 payroll data 的所在位置，或應用程式獲得給它的方式將應用程式。  
  
 詞彙*資料來源*不應混淆與類似的詞彙。 在本手冊中， *DBMS*或是*資料庫*是指資料庫程式或引擎。 進一步區分*桌面的資料庫*設計在個人電腦上執行，且通常加改編，完整的 SQL 和交易支援和*server 資料庫*設計成在用戶端執行 /伺服器的情況並以獨立的資料庫引擎和豐富的 SQL 和交易支援。 *資料庫*也是指特定集合的資料，例如 SQL Server 上的 Xbase 檔案目錄或資料庫中的集合。 它通常相當於這個詞彙*目錄中，* 本手冊中或一詞在其他地方使用*限定詞*在舊版的 ODBC。  
  
 此章節包含下列主題。  
  
-   [資料來源的類型](../../odbc/reference/types-of-data-sources.md)  
  
-   [使用資料來源](../../odbc/reference/using-data-sources.md)  
  
-   [資料來源範例](../../odbc/reference/data-source-example.md)
