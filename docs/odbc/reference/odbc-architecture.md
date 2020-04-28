---
title: ODBC 架構 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC architecture [ODBC], components
- ODBC architecture [ODBC]
ms.assetid: 2604f492-587b-4a51-9876-59a7870b3ef2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 07435dc1a5fbe800f2260e914f315cfe93dd8d1b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305129"
---
# <a name="odbc-architecture"></a>ODBC 架構
ODBC 架構有四個元件：  
  
-   **應用程式**執行處理並呼叫 ODBC 函式，以提交 SQL 語句並取得結果。  
  
-   **驅動程式管理員**代表應用程式載入及卸載驅動程式。 會處理 ODBC 函數呼叫，或將它們傳遞至驅動程式。  
  
-   **驅動程式**會處理 ODBC 函式呼叫、將 SQL 要求提交至特定資料來源，並將結果傳回給應用程式。 必要時，驅動程式會修改應用程式的要求，使要求符合相關 DBMS 所支援的語法。  
  
-   **資料來源**包含使用者想要存取的資料，以及其相關聯的作業系統、DBMS 和用來存取 DBMS 的網路平臺（如果有的話）。  
  
 請注意下列有關 ODBC 架構的要點。 首先，可以存在多個驅動程式和資料來源，讓應用程式能夠同時存取多個資料來源中的資料。 第二，ODBC API 用於兩個位置：應用程式和驅動程式管理員之間，以及驅動程式管理員與每個驅動程式之間。 驅動程式管理員和驅動程式之間的介面，有時稱為「*服務提供者介面*」或*SPI*。 若為 ODBC，應用程式開發介面（API）和服務提供者介面（SPI）是相同的;也就是說，驅動程式管理員和每個驅動程式都具有相同功能的相同介面。  
  
 此章節包含下列主題。  
  
-   [應用程式](../../odbc/reference/applications.md)  
  
-   [驅動程式管理員](../../odbc/reference/the-driver-manager.md)  
  
-   [驅動程式](../../odbc/reference/drivers.md)  
  
-   [資料來源](../../odbc/reference/data-sources.md)
