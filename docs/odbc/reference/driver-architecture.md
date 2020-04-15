---
title: 驅動程式體系結構 |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ffe2023f028357468700b9bd995d22129ba06817
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294218"
---
# <a name="driver-architecture"></a>驅動程式架構
驅動程式體系結構分為兩類,具體取決於哪個軟體處理 SQL 語句:  
  
-   **基於檔案的驅動程式**驅動程式直接存取物理數據。 在這種情況下,驅動程式同時充當驅動程式和數據源;因此,驅動程式充當驅動程序和數據源。也就是說,它處理ODBC調用和SQL語句。 例如,dBASE 驅動程式是基於檔的驅動程式,因為 dBASE 不提供驅動程式可以使用的獨立資料庫引擎。 請務必注意,基於檔的驅動程式的開發人員必須編寫自己的資料庫引擎。  
  
-   **基於 DBMS 驅動程式**驅動程式通過單獨的資料庫引擎訪問物理數據。 在這種情況下,驅動程式僅處理 ODBC 調用;因此,驅動程式將僅處理 ODBC 調用。它將 SQL 語句傳遞給資料庫引擎進行處理。 例如,Oracle 驅動程式是基於 DBMS 的驅動程式,因為 Oracle 具有驅動程式使用的獨立資料庫引擎。 資料庫引擎所在的位置無關緊要。 它可以與驅動程式或網路上的其他計算機駐留在同一台計算機上;它甚至可能通過網關訪問。  
  
 驅動程序體繫結構通常只對驅動程式編寫者感興趣;也就是說,驅動程式體系結構通常對應用程式沒有影響。 但是,體系結構可能會影響應用程式是否可以使用特定於 DBMS 的 SQL。 例如,Microsoft Access 提供了一個獨立的資料庫引擎。 如果 Microsoft Access 驅動程式基於 DBMS -它透過此引擎存取資料 -應用程式可以將 Microsoft Access-SQL 語句傳遞給引擎進行處理。  
  
 但是,如果驅動程式是基於檔的 -也就是說,它包含直接訪問 Microsoft® Access .mdb 檔的專有引擎-任何將特定於 Microsoft 訪問的 SQL 語句傳遞給引擎的嘗試都可能導致語法錯誤。 原因是專有引擎可能僅實現ODBC SQL。  
  
 此章節包含下列主題。  
  
-   [以檔案為基礎的驅動程式](../../odbc/reference/file-based-drivers.md)  
  
-   [以 DBMS 為基礎的驅動程式](../../odbc/reference/dbms-based-drivers.md)  
  
-   [網路範例](../../odbc/reference/network-example.md)  
  
-   [其他驅動程式架構](../../odbc/reference/other-driver-architectures.md)
