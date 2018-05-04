---
title: ODBC 架構 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ODBC architecture [ODBC], components
- ODBC architecture [ODBC]
ms.assetid: 2604f492-587b-4a51-9876-59a7870b3ef2
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 59076df0044feea340c54df8af78bc286afba96b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="odbc-architecture"></a>ODBC 架構
ODBC 架構包含四個元件：  
  
-   **應用程式**執行處理 」 和 「 呼叫 ODBC 函數來提交 SQL 陳述式並擷取結果。  
  
-   **驅動程式管理員**載入和卸載代表應用程式的驅動程式。 處理程序的 ODBC 函數呼叫，或將其傳遞至驅動程式。  
  
-   **驅動程式**處理程序的 ODBC 函數呼叫、 提交 SQL 要求特定資料來源，並將結果傳回到應用程式。 必要時，驅動程式會修改應用程式的要求，使要求符合相關聯的 DBMS 所支援的語法。  
  
-   **資料來源**Consists 資料的使用者想要存取與它關聯中的作業系統，DBMS，以及用來存取 DBMS 的網路平台 （如果有的話）。  
  
 請注意下列有關 ODBC 架構的重點。 第一個、 多個驅動程式和資料來源可以存在，可讓應用程式同時從多個資料來源存取資料。 其次，使用 ODBC API 在兩個地方： 應用程式和驅動程式管理員，以及驅動程式管理員與每個驅動程式之間。 驅動程式管理員與驅動程式之間的介面有時稱為*服務提供者介面，*或*SPI*。 若是 ODBC，應用程式發展介面 (API) 和服務提供者介面 (SPI) 都相同。也就是說，驅動程式管理員和每個驅動程式有相同的函式相同的介面。  
  
 此章節包含下列主題。  
  
-   [應用程式](../../odbc/reference/applications.md)  
  
-   [驅動程式管理員](../../odbc/reference/the-driver-manager.md)  
  
-   [驅動程式](../../odbc/reference/drivers.md)  
  
-   [資料來源](../../odbc/reference/data-sources.md)
