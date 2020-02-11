---
title: 架構視圖 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- schema views [ODBC]
- functions [ODBC], catalog functions
- catalog functions [ODBC], schema views
ms.assetid: f1dfb3e8-a7bd-46c3-92b6-c19531e8409d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1e2dd512ab529f1fb5d216f4a2e459cd601d40e8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67943750"
---
# <a name="schema-views"></a>結構描述檢視
應用程式可以藉由呼叫 ODBC 目錄函數或使用 INFORMATION_SCHEMA views，從 DBMS 抓取中繼資料資訊。 這些視圖是由 ANSI SQL-92 標準所定義。  
  
 如果 DBMS 和驅動程式支援，INFORMATION_SCHEMA views 提供比 ODBC 目錄函數提供更強大且完整的方法來抓取中繼資料。 應用程式可以對其中一個視圖執行自己的自訂**SELECT**語句、可以聯結視圖，或在 views 上執行聯集。 雖然提供更大的公用程式和更廣泛的中繼資料，但 DBMS 不常支援 INFORMATION_SCHEMA 的觀點。 這可能會因為 Dbms 和驅動程式達到 SQL-92 的相容性而變更。  
  
 為了判斷支援哪些視圖，應用程式會使用 SQL_INFO_SCHEMA_VIEWS 選項來呼叫**SQLGetInfo** 。 若要從支援的視圖抓取中繼資料，應用程式會執行**SELECT**語句，以指定所需的架構資訊。
