---
title: 桌面資料庫驅動程式架構 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], architecture
- ODBC desktop database drivers [ODBC], architecture
- desktop database drivers [ODBC], architecture
ms.assetid: 8b4d13f7-ab37-40b4-a9c6-145e7385352f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ae6fb72bb3ed0a9bca1571eb572bbfbd20fe9995
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81288738"
---
# <a name="desktop-database-drivers-architecture"></a>桌面資料庫驅動程式架構
這些驅動程式是設計用來在 Microsoft Windows 95 或更新版本，或是 Windows NT 4.0 和 Windows 2000 上使用。 Windows 95 或更新版本僅支援32位應用程式;Windows NT 4.0 和 Windows 2000 支援16位和32位應用程式。  
  
> [!NOTE]  
>  如需有關要與這些驅動程式搭配使用之 ODBC 版本的資訊，請參閱 ODBC 程式設計*人員參考*，以及過去和目前的版本資訊。 除了已注明的區域之外，這些驅動程式會符合 ODBC 程式設計*人員的參考*。  
  
 ODBC 桌面資料庫驅動程式包含適用于 Microsoft Access、dBASE、Microsoft Excel、Paradox 和 Text 的32位驅動程式。 不包含16位驅動程式。 （Microsoft FoxPro 的驅動程式可分別使用）。  
  
 Windows 95 或更新版本上的應用程式/驅動程式架構為：  
  
 ![應用程式&#47;驅動程式架構： Windows 95 和更新版本](../../odbc/microsoft/media/odbcjetarch1.gif "ODBCJetArch1")  
  
 Windows 95 上的16位應用程式不支援使用這些驅動程式。  
  
 Windows NT 4.0 和 Windows 2000 的應用程式/驅動程式架構為：  
  
 ![應用程式&#47;驅動程式架構： NT 4.0 和 Windows 2000](../../odbc/microsoft/media/odbcjetarch2.gif "ODBCJetArch2")  
  
 桌面資料庫驅動程式是兩層式的驅動程式。 在兩層式設定中，驅動程式不會執行剖析、驗證、優化及執行查詢的進程。 相反地，Microsoft Jet 會執行這些工作。 它會處理 ODBC API 呼叫，並作為 SQL 引擎。 Microsoft Jet 已成為分不開的一部分：驅動程式隨附于驅動程式，並與驅動程式一起存放，即使電腦上沒有其他應用程式使用它。  
  
 桌面資料庫驅動程式包含了六種不同的驅動程式，或更精確的一個驅動程式檔案（Odbcjt32 .dll），而 ODBC[驅動程式管理員](../../odbc/reference/the-driver-manager.md)會使用六種不同的方式。 資料來源的登錄專案中的 DRIVERID 旗標會決定驅動程式管理員使用 Odbcjt32 中的哪一個驅動程式。 應用程式會在呼叫**SQLDriverConnect**所包含的連接字串中傳遞此旗標。 根據預設，旗標是 Microsoft Access 驅動程式的識別碼。  
  
 驅動程式安裝檔會在安裝時變更 DRIVERID 旗標。 除了 Microsoft Access 驅動程式以外的所有驅動程式都有相關聯的安裝程式 DLL。 當您在資料來源的[MICROSOFT ODBC 資料來源管理員](../../odbc/admin/odbc-data-source-administrator.md)中按一下 [**設定**] 時，ODBC 安裝程式 dll （Odbcinst）會載入安裝程式 dll。 安裝程式 DLL 會匯出 ODBC 安裝程式函數**SQLConfigDataSource**。 如果將視窗控制碼傳遞給**SQLConfigDataSource**，此函式會顯示安裝視窗，並根據從使用者介面中選取的驅動程式來變更 DRIVERID 旗標。  
  
 以程式設計方式建立檔案時，會將 Null 視窗控制碼傳遞至**SQLConfigDataSource**，而函式會動態建立資料來源，並根據函式呼叫中的*lpszDriver*引數變更 DRIVERID 旗標。  
  
 Odbcjt32 會在 Microsoft Jet API 之上執行 ODBC 函數。 不過，ODBC 和 Microsoft Jet 函式之間沒有直接的對應。 許多因素（例如資料指標模型和 SQL 對應）會防止函式直接相互關聯。  
  
 ODBC 驅動程式位於 Microsoft Jet 引擎和 ODBC 驅動程式管理員之間。 應用程式所呼叫的某些 ODBC 函式會由驅動程式管理員處理，而不會傳遞至驅動程式。 針對這些函式，Microsoft Jet 永遠不會看到函式呼叫，因為它沒有與驅動程式管理員的直接連接。
