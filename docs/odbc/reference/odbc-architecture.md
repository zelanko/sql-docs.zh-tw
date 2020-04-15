---
title: ODBC 架構 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305129"
---
# <a name="odbc-architecture"></a>ODBC 架構
ODBC 架構結構有四個元件:  
  
-   **套用**執行處理並調用 ODBC 函數以提交 SQL 語句並檢索結果。  
  
-   **驅動程式管理員**代表應用程式載入和卸載驅動程式。 處理ODBC函數調用或將其傳遞給驅動程式。  
  
-   **驅動程式**處理 ODBC 函數調用,向特定數據來源提交 SQL 請求,並將結果返回給應用程式。 如有必要,驅動程式將修改應用程式的請求,以便請求符合關聯的 DBMS 支援的語法。  
  
-   **資料來源**由使用者想要訪問的數據及其關聯的作業系統、DBMS 和網路平臺(如果有)組成,用於訪問 DBMS。  
  
 請注意有關 ODBC 體系結構的以下幾點。 首先,可以存在多個驅動程式和數據源,這允許應用程序同時訪問來自多個數據源的數據。 其次,ODBC API 在兩個位置使用:在應用程式和驅動程式管理器之間,以及驅動程式管理器和每個驅動程序之間。 驅動程式管理員與驅動程式之間的介面有時稱為*服務提供者介面或* *SPI*。 對於 ODBC,應用程式程式設計介面 (API) 和服務提供者介面 (SPI) 相同;即,驅動程式管理器和每個驅動程式具有相同的函數介面。  
  
 此章節包含下列主題。  
  
-   [應用程式](../../odbc/reference/applications.md)  
  
-   [驅動程式管理員](../../odbc/reference/the-driver-manager.md)  
  
-   [驅動程式](../../odbc/reference/drivers.md)  
  
-   [資料來源](../../odbc/reference/data-sources.md)
