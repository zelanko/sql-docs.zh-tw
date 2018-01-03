---
title: "OLE DB 提供者 (ADO) |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- OLE DB providers [ADO]
- ADO, OLE DB providers
ms.assetid: 6e0488c3-934d-4976-99dc-65c580dc7a3c
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d16d75565f0488f641d10a46ea63e87cf184af8a
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="ole-db-providers-ado"></a>OLE DB 提供者 (ADO)
OLE DB 定義一組 COM 介面，可提供應用程式統一存取各種資訊來源中所儲存的資料。 這個方法可讓共用支援的 DBMS 功能至資料來源的適當數量的介面透過其資料的資料來源。 根據設計，高效能架構的 OLE DB 會依據其彈性，以元件為基礎的服務模型的使用情形。 而不是讓應用程式和資料之間的中繼層級低於指定的數目，OLE DB 需求只做為所需的許多元件完成特定工作。  
  
 例如，假設使用者想要執行查詢。 請考慮下列案例：  
  
-   在關聯式資料庫中目前存在的 ODBC 驅動程式，但沒有原生 OLE DB 提供者所在的資料： 應用程式使用 ADO 與 OLE DB Provider for ODBC，後者接著會載入適當的 ODBC 驅動程式。 驅動程式會將 SQL 陳述式傳遞至 DBMS，擷取資料。  
  
-   原生的 OLE DB 提供者是 Microsoft SQL Server 中的資料所在： 應用程式會使用 ADO 來向直接 OLE DB Provider for Microsoft SQL Server。 需要的任何媒介不。  
  
-   資料位於 Microsoft Exchange Server 的 OLE DB 提供者，但這不會公開程序的 SQL 查詢引擎： 應用程式適用於 Microsoft Exchange 與 OLE DB 提供者會使用 ADO 和 OLE DB 查詢處理器會呼叫處理查詢的元件。  
  
-   資料位於 Microsoft NTFS 檔案系統格式的文件： 透過 Microsoft 索引服務，以啟用有效的內容檔案系統中索引的內容和文件的屬性以原生的 OLE DB 提供者存取資料搜尋。  
  
 在所有先前範例中，應用程式可以查詢資料。 使用元件的最小數目，則符合使用者的需求。 在每個案例中，才需要請使用其他元件和必要的元件會叫用。 使用 OLE DB 時大幅高效能提供可重複使用及共用元件的這個需求載入。  
  
 提供者分為兩類： 所提供的資料以及提供服務。 資料提供者擁有它自己的資料，且會公開在表格式表單，以您的應用程式。 服務提供者封裝服務所產生及取用資料，加強 ADO 應用程式中的功能。 服務提供者也可以進一步定義做為服務元件，必須與其他服務提供者或元件搭配運作。  
  
 ADO 提供一致，較高的層級介面，以各種 OLE DB 提供者。  
  
 此章節包含下列主題。  
  
-   [資料提供者](../../../ado/guide/data/data-providers.md)  
  
-   [服務提供者和元件](../../../ado/guide/data/service-providers-and-components.md)
