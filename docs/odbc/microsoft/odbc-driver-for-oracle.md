---
title: 甲骨文的ODBC驅動程式 |微軟文件
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
ms.openlocfilehash: 2b5f1aabd23a587e681c33aed4b4119523444219
ms.sourcegitcommit: fc5b757bb27048a71bb39755648d5cefe25a8bc6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "80402616"
---
# <a name="odbc-driver-for-oracle"></a>ODBC Driver for Oracle
> [!IMPORTANT]  
>  此功能將在將來版本的 Windows 中刪除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 而是使用[Oracle 提供的 ODBC 驅動程式](https://www.oracle.com/database/technologies/releasenote-odbc-ic.html)。  
  
 Microsoft® Oracle 的 ODBC 驅動程式允許您將符合 ODBC 的應用程式連接到 Oracle 資料庫。 Oracle 的 ODBC 驅動程式符合*ODBC 程式師參考*中所述的開放資料庫連接 (ODBC) 規範。 它允許從 Internet 資訊服務 (IIS) 存取 PL/SQL 包、XA/DTC 整合和 Oracle 存取。  
  
 Oracle RDBMS 是一個多使用者關係資料庫管理系統,可運行各種工作站和微型電腦操作系統。 運行 Microsoft Windows 的 IBM 相容電腦可以通過網路與 Oracle 資料庫伺服器進行通信。 支援的網路包括微軟局域網管理器、網華、VINES、DECnet 以及任何支援 TCP/IP 的網路。  
  
 Oracle 的 ODBC 驅動程式使應用程式能夠透過 ODBC 介面存取 Oracle 資料庫中的數據。 驅動程式可以存取本地 Oracle 資料庫,也可以通過 SQL_Net與網路通訊。 下圖詳細介紹了此應用程式和驅動程序體系結構。  
  
 ![Oracle 應用程式的 ODBC 驅動程式&#47;驅動程式架構結構](../../odbc/microsoft/media/orcdrvsdkarch.gif "OrcDrvSDKArch")  
  
 Oracle 的 ODBC 驅動程式符合 API 符合等級 1 和 SQL 一致性級別核心。 它還支援 API 一致性級別 2 中的某些函數以及核心和擴展 SQL 一致性級別中的大部分語法。 該驅動程式符合 ODBC 2.5 標準,支援 32 位元系統。 完全支援 Oracle 7.3x;Oracle8 的支援有限。 Oracle 的 ODBC 驅動程式不支援任何新的 Oracle8 資料類型 - Unicode 資料類型、BB、CLOB 等 , 也不支援 Oracle 新的關係物件模型。 有關支援的資料類型的詳細資訊,請參考本指南中[支援的類型](../../odbc/microsoft/supported-data-types-odbc-driver-for-oracle.md)。  
  
 要存取 Oracle 資料,需要以下元件:  
  
-   甲骨文的 ODBC 驅動程式  
  
-   甲骨文RDBMS資料庫  
  
-   甲骨文用戶端軟體  
  
 此外,對於遠端連線:  
  
-   連接運行驅動程式和資料庫的計算機的網路。 網路必須支援SQL_Net連接。  
  
## <a name="component-documentation"></a>元件文件  
 本指南包含有關為 Oracle 設定和設定 Microsoft ODBC 驅動程式以及添加程式設計功能的詳細資訊。 它還包含技術參考材料。  
  
 有關特定 Oracle 產品行為的資訊,請參閱隨 Oracle 產品隨附的文檔。  
  
 有關使用 ODBC 資料來源管理員為 Oracle 設定或設定 Microsoft ODBC 驅動程式的資訊,請參閱[ODBC 資料來源管理員](../../odbc/admin/odbc-data-source-administrator.md)文件。  
  
 此章節包含下列主題。  
  
-   [ODBC Driver for Oracle 使用者指南](../../odbc/microsoft/odbc-driver-for-oracle-user-s-guide.md)  
  
-   [ODBC Driver for Oracle 程式設計人員參考](../../odbc/microsoft/odbc-driver-for-oracle-programmer-s-reference.md)
