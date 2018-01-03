---
title: "桌面資料庫驅動程式架構 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], architecture
- ODBC desktop database drivers [ODBC], architecture
- desktop database drivers [ODBC], architecture
ms.assetid: 8b4d13f7-ab37-40b4-a9c6-145e7385352f
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3f5c7b12e5413441476e70dc63fe9d3da9284635
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="desktop-database-drivers-architecture"></a>桌面資料庫驅動程式架構
這些驅動程式專為使用 Microsoft Windows 95 上或更新版本中，或 Windows NT 4.0 和 Windows 2000。 只有 32 位元應用程式支援 Windows 95 或更新版本。16 位元和 32 位元應用程式都支援 Windows NT 4.0 和 Windows 2000。  
  
> [!NOTE]  
>  如要這些驅動程式搭配使用的 ODBC 版本的相關資訊，請參閱*ODBC 程式設計人員參考*，和過去和目前的版本資訊。 除了標註的區域，這些驅動程式符合*ODBC 程式設計人員參考*。  
  
 ODBC 桌面資料庫驅動程式包含 32 位元驅動程式，如 Microsoft Access、 dBASE、 Microsoft Excel、 Paradox 和文字。 無 16 位元驅動程式會包含項目。 （用於 Access 的驅動程式是使用分開）。  
  
 在 Windows 95 或更新版本的應用程式/驅動程式架構是：  
  
 ![應用程式 &#47; 驅動程式架構： Windows 95 和更新版本](../../odbc/microsoft/media/odbcjetarch1.gif "ODBCJetArch1")  
  
 不支援這些驅動程式在 Windows 95 上的 16 位元應用程式的使用。  
  
 是 Windows NT 4.0 和 Windows 2000 上的應用程式/驅動程式架構：  
  
 ![應用程式 &#47; 驅動程式架構： NT 4.0 和 Windows 2000](../../odbc/microsoft/media/odbcjetarch2.gif "ODBCJetArch2")  
  
 桌面資料庫驅動程式是兩層式驅動程式。 在兩層式組態中，驅動程式不會執行剖析、 驗證、 最佳化及執行查詢的程序。 相反地，Microsoft Jet 執行這些工作。 它會處理 ODBC API 呼叫，並做為 SQL 引擎。 Microsoft Jet 變得有一個整數、 密不可分的部分驅動程式： 它隨附於驅動程式，且位於與驅動程式，即使在電腦上的沒有其他應用程式會使用它。  
  
 桌面資料庫驅動程式包含六個不同的驅動程式，或一個驅動程式檔案 (Odbcjt32.dll) 的更精確地說，ODBC[驅動程式管理員](../../odbc/reference/the-driver-manager.md)使用六個不同的方式。 DRIVERID 中的旗標的資料來源的登錄項目決定哪一個驅動程式中 Odbcjt32.dll 驅動程式管理員使用。 應用程式中呼叫包含在連接字串中傳遞此旗標**SQLDriverConnect**。 根據預設，此旗標是 Microsoft Access 驅動程式的識別碼。  
  
 驅動程式安裝程式檔案於安裝時期變更 DRIVERID 旗標。 除了 Microsoft Access 驅動程式的所有驅動程式具有相關聯的安裝程式 DLL。 當您按一下**安裝**中[Microsoft ODBC 資料來源管理員](../../odbc/admin/odbc-data-source-administrator.md)針對資料來源，ODBC 安裝程式 DLL (Odbcinst.dll) 載入安裝程式 DLL。 安裝程式 DLL 匯出 ODBC 安裝程式函式**SQLConfigDataSource**。 如果視窗控制代碼傳遞至**SQLConfigDataSource**，此函式會顯示安裝程式視窗，並變更 DRIVERID 旗標，根據從使用者介面中選取的驅動程式。  
  
 NULL 視窗控制代碼時以程式設計方式建立的檔案傳遞至**SQLConfigDataSource**，函式會建立資料來源，以動態方式變更根據 DRIVERID 旗標和*lpszDriver*函式呼叫中的引數。  
  
 Odbcjt32.dll 實作 Microsoft Jet API 之上的 ODBC 函數。 但是 ODBC 和 Microsoft Jet 函式之間沒有直接對應。 許多因素，例如資料指標模型和 SQL 對應，避免直接的相互關聯的函式。  
  
 ODBC 驅動程式位於 Microsoft Jet 引擎和 ODBC 驅動程式管理員之間。 在應用程式呼叫某些 ODBC 函數處理由驅動程式管理員和未傳遞至驅動程式。 這些函式中，Microsoft Jet 永遠看不到函式呼叫，因為它並沒有直接連線到驅動程式管理員。
