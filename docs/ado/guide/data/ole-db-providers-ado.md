---
description: OLE DB 提供者 (ADO)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 7fb247f62173a0c622a08eb2d55af005efcb2669
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/25/2020
ms.locfileid: "88805679"
---
# <a name="ole-db-providers-ado"></a>OLE DB 提供者 (ADO)
OLE DB 定義一組 COM 介面，讓應用程式能夠統一存取儲存在不同資訊來源中的資料。 這種方法可讓資料來源透過支援適用于資料來源之 DBMS 功能數量的介面來共用其資料。 根據設計，OLE DB 的高效能架構是以其使用彈性、元件為基礎的服務模型為基礎。 除了在應用程式和資料之間擁有指定數目的中介層，OLE DB 只需要需要多少元件才能完成特定工作。  
  
 例如，假設使用者想要執行查詢。 請考慮下列案例：  
  
-   資料位於目前存在 ODBC 驅動程式但沒有原生 OLE DB 提供者的關係資料庫中：應用程式會使用 ADO 來與 ODBC 的 OLE DB 提供者交談，然後載入適當的 ODBC 驅動程式。 驅動程式會將 SQL 語句傳遞至 DBMS，以抓取資料。  
  
-   資料位於有原生 OLE DB 提供者的 Microsoft SQL Server：應用程式會使用 ADO 來直接與 OLE DB 提供者交談以進行 Microsoft SQL Server。 不需要任何媒介。  
  
-   資料位於 Microsoft Exchange Server 中，其中有 OLE DB 提供者，但未公開引擎來處理 SQL 查詢：應用程式會使用 ADO 來與 Microsoft Exchange 的 OLE DB 提供者交談，並在 OLE DB 查詢處理器元件上呼叫以處理查詢。  
  
-   資料會以檔案格式位於 Microsoft NTFS 檔案系統中：使用原生 OLE DB 提供者透過 Microsoft 索引服務存取資料，此服務會編制檔案系統中檔的內容和屬性的索引，以啟用有效率的內容搜尋。  
  
 在上述所有範例中，應用程式都可以查詢資料。 以最小的元件數目來滿足使用者的需求。 在每個情況下，只有在需要時才會使用其他元件，而且只會叫用必要的元件。 當使用 OLE DB 時，此要求載入可重複使用且可共用的元件會大幅提高效能。  
  
 提供者分為兩種類別：提供資料的資料，以及提供服務的資料。 資料提供者擁有本身的資料，並以表格形式以表格形式公開給您的應用程式。 服務提供者會藉由產生和取用資料來封裝服務，以增強 ADO 應用程式中的功能。 服務提供者也可以進一步定義為服務元件，該元件必須與其他服務提供者或元件搭配使用。  
  
 ADO 提供一致、更高層級的介面給各種 OLE DB 提供者。  
  
 此章節包含下列主題。  
  
-   [資料提供者](./data-providers.md)  
  
-   [服務提供者和元件](./service-providers-and-components.md)