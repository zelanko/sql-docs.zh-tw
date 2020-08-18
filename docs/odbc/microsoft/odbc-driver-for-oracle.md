---
description: ODBC Driver for Oracle
title: 適用于 Oracle 的 ODBC 驅動程式 |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a561539ff960dfa6691d26496b1b62d2ee8ae763
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449330"
---
# <a name="odbc-driver-for-oracle"></a>ODBC Driver for Oracle
> [!IMPORTANT]  
>  未來的 Windows 版本將會移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 請改用 Oracle 提供的 ODBC 驅動程式。  
  
 適用于 Oracle 的 Microsoft® ODBC 驅動程式可讓您將 ODBC 相容的應用程式連接到 Oracle 資料庫。 ODBC Driver for Oracle 符合 Odbc 程式設計 *人員參考*中所述 (odbc) 規格的開放式資料庫連接。 它可讓您從 Internet Information Services (IIS) 存取 PL/SQL 套件、XA/DTC 整合和 Oracle 存取。  
  
 Oracle RDBMS 是一種多使用者關係資料庫管理系統，可搭配各種工作站和 minicomputer 作業系統來執行。 執行 Microsoft Windows 的 IBM 相容電腦可以透過網路與 Oracle 資料庫伺服器通訊。 支援的網路包括 Microsoft LAN Manager、NetWare、VINES、DECnet，以及任何支援 TCP/IP 的網路。  
  
 ODBC Driver for Oracle 可讓應用程式透過 ODBC 介面存取 Oracle 資料庫中的資料。 驅動程式可以存取本機 Oracle 資料庫，也可以透過 SQL * Net 與網路通訊。 下圖詳細說明此應用程式和驅動程式架構。  
  
 ![ODBC Driver for Oracle app&#47;驅動程式架構](../../odbc/microsoft/media/orcdrvsdkarch.gif "OrcDrvSDKArch")  
  
 ODBC Driver for Oracle 符合「API 一致性層級1」和「SQL 一致性層級核心」。 它也支援 API 一致性層級2中的一些函數，以及核心和延伸 SQL 一致性層級中的大部分文法。 驅動程式符合 ODBC 2.5 規範，並支援32位系統。 Oracle 7.3 x 完全受到支援;Oracle8 的支援有限。 ODBC Driver for Oracle 不支援任何新的 Oracle8 資料類型，也就是 Unicode 資料類型、Blob、Clob 等等，也不支援 Oracle 的新關係物件模型。 如需有關支援的資料類型的詳細資訊，請參閱本指南中 [支援的資料類型](../../odbc/microsoft/supported-data-types-odbc-driver-for-oracle.md) 。  
  
 若要存取 Oracle 資料，需要下列元件：  
  
-   ODBC Driver for Oracle  
  
-   Oracle RDBMS 資料庫  
  
-   Oracle 用戶端軟體  
  
 此外，針對遠端連線：  
  
-   連接執行驅動程式和資料庫之電腦的網路。 網路必須支援 SQL * Net 連接。  
  
## <a name="component-documentation"></a>元件檔  
 本指南包含設定和設定 Microsoft ODBC Driver for Oracle 以及加入程式設計功能的詳細資訊。 它也包含技術參考資料。  
  
 如需有關特定 Oracle 產品行為的詳細資訊，請參閱 Oracle 產品隨附的檔。  
  
 如需使用「ODBC 資料來源管理員」來設定或設定 Microsoft ODBC Driver for Oracle 的詳細資訊，請參閱「 [Odbc 資料來源管理員](../../odbc/admin/odbc-data-source-administrator.md) 」檔。  
  
 此章節包含下列主題。  
  
-   [ODBC Driver for Oracle 使用者指南](../../odbc/microsoft/odbc-driver-for-oracle-user-s-guide.md)  
  
-   [ODBC Driver for Oracle 程式設計人員參考](../../odbc/microsoft/odbc-driver-for-oracle-programmer-s-reference.md)
