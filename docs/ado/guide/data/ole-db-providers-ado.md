---
title: OLE DB 提供者（ADO） |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 1a50ad68f7a4b40d008bd6d60b6d24e1984428e1
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82759134"
---
# <a name="ole-db-providers-ado"></a>OLE DB 提供者 (ADO)
OLE DB 定義一組 COM 介面，讓應用程式能夠以一致的方式存取儲存在不同資訊來源中的資料。 這種方法可讓資料來源透過支援資料來源適當之 DBMS 功能數量的介面來共用其資料。 根據設計，OLE DB 的高效能架構是以彈性、以元件為基礎的服務模型的使用為基礎。 OLE DB 不會在應用程式與資料之間擁有指定的仲介層數目，而是只需要所需的元件數量，才能完成特定工作。  
  
 例如，假設使用者想要執行查詢。 請考慮下列案例：  
  
-   資料位於關係資料庫中，目前已有 ODBC 驅動程式，但沒有原生 OLE DB 提供者：應用程式會使用 ADO 與 ODBC 的 OLE DB 提供者溝通，然後載入適當的 ODBC 驅動程式。 驅動程式會將 SQL 語句傳遞至 DBMS，以抓取資料。  
  
-   資料位於具有原生 OLE DB 提供者的 Microsoft SQL Server 中：應用程式會使用 ADO 直接與 Microsoft SQL Server 的 OLE DB 提供者交談。 不需要任何媒介。  
  
-   資料位於 Microsoft Exchange Server 中，其中有 OLE DB 提供者，但未公開引擎來處理 SQL 查詢：應用程式會使用 ADO 與 Microsoft Exchange 的 OLE DB 提供者溝通，並在 OLE DB 查詢處理器元件上呼叫以處理查詢。  
  
-   資料是以檔案格式存放在 Microsoft NTFS 檔案系統中：資料是透過使用原生 OLE DB 提供者透過 Microsoft 索引服務來存取的，這會在檔案系統中編制檔內容和屬性的索引，以啟用有效率的內容搜尋。  
  
 在上述所有範例中，應用程式都可以查詢資料。 以最小的元件數目來符合使用者的需求。 在每個案例中，只有在必要時才會使用其他元件，而且只會叫用必要的元件。 當使用 OLE DB 時，可重複使用和可共用元件的這項需求可大幅提高效能。  
  
 提供者分成兩個類別：提供資料和提供服務的人員。 資料提供者擁有自己的資料，並以表格式形式將它公開給您的應用程式。 服務提供者會藉由產生和取用資料，在您的 ADO 應用程式中擴充功能來封裝服務。 服務提供者也可以進一步定義為服務元件，這必須與其他服務提供者或元件搭配使用。  
  
 ADO 為各種 OLE DB 提供者提供一致、更高層級的介面。  
  
 此章節包含下列主題。  
  
-   [資料提供者](../../../ado/guide/data/data-providers.md)  
  
-   [服務提供者和元件](../../../ado/guide/data/service-providers-and-components.md)
