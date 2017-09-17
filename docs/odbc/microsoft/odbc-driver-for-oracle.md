---
title: "Oracle 的 ODBC 驅動程式 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC driver for Oracle [ODBC]
- ODBC driver for Oracle [ODBC], about ODBC driver for Oracle
- Oracle data access [ODBC]
ms.assetid: 937e0662-8b1d-44f7-b077-4015c6605b2c
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e66dd7ed6406287c0fb4e6722d8b5915428f705b
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="odbc-driver-for-oracle"></a>Oracle 的 ODBC 驅動程式
> [!IMPORTANT]  
>  將移除這項功能，在未來的版本的 Windows。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 相反地，使用由 Oracle 提供的 ODBC 驅動程式。  
  
 Oracle 的 Microsoft® ODBC 驅動程式可讓您連接到 Oracle 資料庫 ODBC 相容應用程式。 Oracle 的 ODBC 驅動程式是否符合開放式資料庫連接 (ODBC) 規格中所述*ODBC 程式設計人員參考*。 它可讓 PL/SQL 封裝、 XA/DTC 整合，以及 Oracle 存取從網際網路資訊服務 (IIS) 內的存取。  
  
 Oracle RDBMS 是多使用者的關聯式資料庫管理系統所執行的各種工作站和迷你電腦作業系統。 執行 Microsoft Windows 的 IBM 相容電腦可以透過網路通訊與 Oracle 資料庫伺服器。 支援的網路包含 Microsoft LAN Manager、 NetWare、 VINES、 DECnet 和任何支援 TCP/IP 的網路。  
  
 Oracle 的 ODBC 驅動程式可讓應用程式透過 ODBC 介面存取 Oracle 資料庫中的資料。 此驅動程式可以存取本機 Oracle 資料庫或透過 SQL 網路與通訊 * 網路。 下圖詳細說明此應用程式和驅動程式的架構。  
  
 ![ODBC Driver for Oracle 應用程式 &#47; 驅動程式架構](../../odbc/microsoft/media/orcdrvsdkarch.gif "OrcDrvSDKArch")  
  
 Oracle 的 ODBC 驅動程式符合 API 的一致性層級 1 和 SQL 一致性層級的核心。 它也會支援 API 的一致性層級 2 和大部分的核心和擴充 SQL 一致性層級中的文法中的某些函式。 驅動程式為 ODBC 2.5 相容，並支援 32 位元系統。 Oracle 7.3 x 完全; 支援Oracle8 具有有限的支援。 ODBC Driver for Oracle 不支援新的 Oracle8 資料類型，Unicode 資料類型，Blob、 Clob、，依此類推，也不支援 Oracle 的新的關聯式物件模型。 如需有關支援的資料類型的詳細資訊，請參閱[Supported Data Types](../../odbc/microsoft/supported-data-types-odbc-driver-for-oracle.md)本指南中。  
  
 若要存取 Oracle 資料，也需要下列元件：  
  
-   ODBC Driver for Oracle  
  
-   RDBMS Oracle 資料庫  
  
-   Oracle 用戶端軟體  
  
 此外，針對遠端連線：  
  
-   連接執行驅動程式和資料庫之電腦的網路。 網路必須支援 SQL * Net 連線。  
  
## <a name="component-documentation"></a>元件的文件  
 本指南包含關於設定和設定 Microsoft ODBC Driver for Oracle 和新增程式設計功能的詳細的資訊。 它也包含的技術參考資料。  
  
 如需有關特定 Oracle 的產品行為，請參閱 Oracle 產品隨附的文件。  
  
 設定或設定 Microsoft ODBC Driver for Oracle 使用 ODBC 資料來源管理員的相關資訊，請參閱[ODBC 資料來源管理員](../../odbc/admin/odbc-data-source-administrator.md)文件。  
  
 此章節包含下列主題。  
  
-   [ODBC Driver for Oracle 使用者指南](../../odbc/microsoft/odbc-driver-for-oracle-user-s-guide.md)  
  
-   [ODBC Driver for Oracle 程式設計人員參考](../../odbc/microsoft/odbc-driver-for-oracle-programmer-s-reference.md)
