---
description: 桌面資料庫驅動程式架構
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
ms.openlocfilehash: d330392424b683e24f17bd959d0a29e76eedbd36
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449570"
---
# <a name="desktop-database-drivers-architecture"></a>桌面資料庫驅動程式架構
這些驅動程式的設計目的是要使用 Microsoft Windows 95 或更新版本，或 Windows NT 4.0 和 Windows 2000。 Windows 95 或更新版本僅支援32位的應用程式;Windows NT 4.0 和 Windows 2000 支援16位和32位的應用程式。  
  
> [!NOTE]  
>  如需有關要與這些驅動程式搭配使用之 ODBC 版本的詳細資訊，請參閱 Odbc 程式設計 *人員參考*，以及過去和目前的版本資訊。 除了注明的區域之外，這些驅動程式也符合 ODBC 程式設計 *人員的參考*。  
  
 ODBC Desktop 資料庫驅動程式包含適用于 Microsoft Access、dBASE、Microsoft Excel、Paradox 和文字的32位驅動程式。 未包含任何16位驅動程式。  (適用于 Microsoft FoxPro 的驅動程式可分別使用。 )   
  
 Windows 95 或更新版本上的應用程式/驅動程式架構為：  
  
 ![應用程式&#47;驅動程式架構： Windows 95 和更新版本](../../odbc/microsoft/media/odbcjetarch1.gif "ODBCJetArch1")  
  
 不支援 Windows 95 上的16位應用程式使用這些驅動程式。  
  
 Windows NT 4.0 和 Windows 2000 上的應用程式/驅動程式架構為：  
  
 ![應用程式&#47;驅動程式架構： NT 4.0 和 Windows 2000](../../odbc/microsoft/media/odbcjetarch2.gif "ODBCJetArch2")  
  
 桌面資料庫驅動程式是兩層式的驅動程式。 在兩層式設定中，驅動程式不會執行剖析、驗證、優化和執行查詢的進程。 相反地，Microsoft Jet 會執行這些工作。 它會處理 ODBC API 呼叫，並作為 SQL 引擎。 Microsoft Jet 已成為驅動程式的一部分分不開：它隨附于驅動程式，並隨附于驅動程式，即使電腦上沒有其他應用程式使用它。  
  
 桌面資料庫驅動程式是由六種不同的驅動程式所組成，也就是更精確的一個驅動程式檔案 ( # A0) ，ODBC [驅動程式管理員](../../odbc/reference/the-driver-manager.md) 會使用六種不同的方式。 資料來源之登錄專案中的 DRIVERID 旗標會決定驅動程式管理員所使用 Odbcjt32.dll 中的驅動程式。 應用程式會在呼叫 **SQLDriverConnect**所包含的連接字串中傳遞此旗標。 根據預設，旗標是 Microsoft Access 驅動程式的識別碼。  
  
 驅動程式安裝檔會在安裝時期變更 DRIVERID 旗標。 除了 Microsoft Access 驅動程式以外的所有驅動程式都有相關聯的安裝程式 DLL。 當您針對資料來源按一下[MICROSOFT Odbc 資料來源管理員](../../odbc/admin/odbc-data-source-administrator.md)中的 [**安裝程式**] 時，ODBC 安裝程式 dll ( # A0) 會載入安裝程式 dll。 安裝 DLL 會匯出 ODBC 安裝程式函數 **SQLConfigDataSource**。 如果將視窗控制碼傳遞至 **SQLConfigDataSource**，此函式會顯示安裝程式視窗，並根據從使用者介面選取的驅動程式來變更 DRIVERID 旗標。  
  
 以程式設計方式建立檔案時，會將 Null 視窗控制碼傳遞至 **SQLConfigDataSource**，而函式會動態建立資料來源，根據函式呼叫中的 *lpszDriver* 引數來變更 DRIVERID 旗標。  
  
 Odbcjt32.dll 在 Microsoft Jet API 之上執行 ODBC 函數。 不過，ODBC 與 Microsoft Jet 函數之間沒有直接對應。 許多因素（例如資料指標模型和 SQL 對應）都會防止函式的直接相互關聯。  
  
 ODBC 驅動程式位於 Microsoft Jet 引擎和 ODBC 驅動程式管理員之間。 應用程式所呼叫的某些 ODBC 函數是由驅動程式管理員處理，而不會傳遞至驅動程式。 針對這些函式，Microsoft Jet 永遠不會看到函式呼叫，因為它不會直接連接到驅動程式管理員。
