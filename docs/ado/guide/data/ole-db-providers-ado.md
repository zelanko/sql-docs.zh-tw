---
title: OLE DB 提供者 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- OLE DB providers [ADO]
- ADO, OLE DB providers
ms.assetid: 6e0488c3-934d-4976-99dc-65c580dc7a3c
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 926e5abc1c65db152c5ca5927c5acd2c932d6b90
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66700531"
---
# <a name="ole-db-providers-ado"></a>OLE DB 提供者 (ADO)
OLE DB 定義一組 COM 介面，可提供應用程式一致的存取會儲存在各種資訊來源的資料。 這種方法可讓資料來源共用其資料，透過支援的 DBMS 功能到資料來源的適當數量的介面。 根據設計，OLE DB 的高效能架構根據其使用彈性、 以元件為基礎的服務模型。 而不是讓應用程式與資料之間的中繼層的規定的數目，OLE DB 會需要只有在做為所需的許多元件完成特定工作。  
  
 例如，假設使用者想要執行查詢。 請考慮下列案例：  
  
-   資料位於關聯式資料庫目前存在的 ODBC 驅動程式，但沒有原生 OLE DB 提供者：應用程式會使用 ADO 與 OLE DB Provider for ODBC，後者接著會載入適當的 ODBC 驅動程式。 驅動程式會將 SQL 陳述式傳遞至 DBMS，擷取資料。  
  
-   資料位於原生的 OLE DB 提供者是 Microsoft SQL Server:應用程式使用 ADO 與直接 OLE DB Provider for Microsoft SQL Server。 需要任何媒介不。  
  
-   資料會位於 Microsoft Exchange Server 的 OLE DB 提供者，但這不會公開程序的 SQL 查詢引擎：應用程式使用 ADO 與 OLE DB 提供者適用於 Microsoft Exchange，並在處理查詢的 OLE DB 查詢處理器元件時呼叫。  
  
-   資料位於 Microsoft NTFS 檔案系統中的文件形式：透過 Microsoft 索引服務，在檔案系統，以啟用有效的內容搜尋索引的內容和屬性的文件中使用原生的 OLE DB 提供者存取資料。  
  
 在所有前述範例中，應用程式可以查詢的資料。 最小元件數會符合使用者的需求。 在每個案例中，只有當有需要請使用其他元件，並叫用必要的元件。 使用 OLE DB 時，此視需要載入可重複使用及共用元件的大幅高效能貢獻。  
  
 提供者分為兩類： 提供與資料提供服務。 資料提供者擁有它自己的資料，且會公開在表格式的格式，您的應用程式。 服務提供者封裝服務所產生和取用資料，擴充您的 ADO 應用程式中的功能。 服務提供者也可以進一步定義做為服務元件，必須與其他服務提供者或元件搭配運作。  
  
 ADO 提供一致、 較高的層級介面，以各種 OLE DB 提供者。  
  
 此章節包含下列主題。  
  
-   [資料提供者](../../../ado/guide/data/data-providers.md)  
  
-   [服務提供者和元件](../../../ado/guide/data/service-providers-and-components.md)
