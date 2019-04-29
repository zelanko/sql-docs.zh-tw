---
title: ODBC Driver for Oracle |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC]
- ODBC driver for Oracle [ODBC], about ODBC driver for Oracle
- Oracle data access [ODBC]
ms.assetid: 937e0662-8b1d-44f7-b077-4015c6605b2c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4685d209d768bd3ff41c1c7367ef6cb6dcd45bcf
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63043856"
---
# <a name="odbc-driver-for-oracle"></a>ODBC Driver for Oracle
> [!IMPORTANT]  
>  Windows 的未來版本將移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 相反地，使用所提供的 ODBC 驅動程式。  
  
 Microsoft® ODBC Driver for Oracle 可讓您連接到 Oracle 資料庫應用程式符合 ODBC 規範。 ODBC Driver for Oracle 符合開放式資料庫連接 (ODBC) 規格中所述*ODBC 程式設計人員參考*。 它可讓 PL/SQL 封裝、 XA/DTC 整合，以及 Oracle 存取從網際網路資訊服務 (IIS) 內的存取。  
  
 Oracle RDBMS 是執行各種不同的工作站和迷你電腦作業系統的多使用者的關聯式資料庫管理系統。 執行 Microsoft Windows 的 IBM 相容電腦可以與 Oracle 資料庫伺服器透過網路進行通訊。 支援的網路包含 Microsoft LAN Manager、 NetWare、 VINES、 DECnet 和任何支援 TCP/IP 的網路。  
  
 ODBC Driver for Oracle 可讓應用程式透過 ODBC 介面存取 Oracle 資料庫中的資料。 此驅動程式可以存取本機的 Oracle 資料庫，或透過 SQL 網路與通訊 * Net。 下圖詳細說明此應用程式和驅動程式的架構。  
  
 ![Oracle 應用程式的 ODBC 驅動程式&#47;驅動程式架構](../../odbc/microsoft/media/orcdrvsdkarch.gif "OrcDrvSDKArch")  
  
 ODBC Driver for Oracle 符合 API 的一致性層級 1 」 及 「 SQL 一致性層級的核心。 它也會支援 API 的一致性層級 2 和大部分的核心和擴充 SQL 一致性層級中的文法中的某些函式。 驅動程式 ODBC 2.5 相容且支援 32 位元系統。 Oracle 7.3 x 完全; 支援Oracle8 具有有限的支援。 ODBC Driver for Oracle 不支援任何新的 Oracle8 資料類型-Unicode 資料類型、 Blob、 Clob，而且也不支援 Oracle 的新的關聯式物件模型。 如需支援的資料類型的詳細資訊，請參閱 < [Supported Data Types](../../odbc/microsoft/supported-data-types-odbc-driver-for-oracle.md)本指南中。  
  
 若要存取 Oracle 資料，下列元件是必要的：  
  
-   ODBC Driver for Oracle  
  
-   Oracle RDBMS 資料庫  
  
-   Oracle 用戶端軟體  
  
 此外，針對遠端連線：  
  
-   網路連線執行驅動程式和資料庫的電腦。 網路必須支援 SQL * Net 連接。  
  
## <a name="component-documentation"></a>元件的文件  
 本指南包含設定和設定 Microsoft ODBC Driver for Oracle 和新增程式設計功能的詳細的資訊。 它也包含技術參考資料。  
  
 如需特定的 Oracle 產品行為的資訊，請參閱隨附的 Oracle 產品的文件。  
  
 如需安裝或設定 Microsoft ODBC Driver for Oracle 使用 ODBC 資料來源管理員資訊，請參閱[ODBC 資料來源管理員](../../odbc/admin/odbc-data-source-administrator.md)文件。  
  
 此章節包含下列主題。  
  
-   [ODBC Driver for Oracle 使用者指南](../../odbc/microsoft/odbc-driver-for-oracle-user-s-guide.md)  
  
-   [ODBC Driver for Oracle 程式設計人員參考](../../odbc/microsoft/odbc-driver-for-oracle-programmer-s-reference.md)
