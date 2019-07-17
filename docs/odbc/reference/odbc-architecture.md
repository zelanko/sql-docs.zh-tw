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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 781a214d3ca059a442680c332d79aad48914976c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68111225"
---
# <a name="odbc-architecture"></a>ODBC 架構
ODBC 架構有四個元件：  
  
-   **應用程式**執行處理 」 和 「 呼叫 ODBC 函數來提交 SQL 陳述式並擷取結果。  
  
-   **驅動程式管理員**載入和卸載驅動程式，代表應用程式。 處理程序的 ODBC 函數呼叫，或將其傳遞至驅動程式。  
  
-   **驅動程式**程序的 ODBC 函數呼叫、 送出至特定的資料來源，SQL 要求和結果傳回到應用程式。 如有必要，驅動程式會修改應用程式的要求，使要求符合相關聯的 DBMS 所支援的語法。  
  
-   **資料來源**Consists 資料的使用者想要存取和其相關聯中的作業系統、 DBMS 和網路平台 （如果有的話） 用來存取 DBMS。  
  
 請注意下列有關 ODBC 架構的重點。 第一個、 多個驅動程式和資料來源可以存在，可讓應用程式同時從多個資料來源存取資料。 第二，ODBC API 會在兩個地方： 應用程式與驅動程式管理員 中，以及驅動程式管理員和每個驅動程式。 驅動程式管理員和驅動程式之間的介面有時稱為*服務提供者介面，* 或是*SPI*。 若是 ODBC，應用程式發展介面 (API) 和服務提供者介面 (SPI) 都相同;也就是驅動程式管理員和每個驅動程式有相同的函式相同的介面。  
  
 此章節包含下列主題。  
  
-   [應用程式](../../odbc/reference/applications.md)  
  
-   [驅動程式管理員](../../odbc/reference/the-driver-manager.md)  
  
-   [驅動程式](../../odbc/reference/drivers.md)  
  
-   [資料來源](../../odbc/reference/data-sources.md)
