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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7487d073b95190418ee7f6900390a2d60ce42e13
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62629053"
---
# <a name="desktop-database-drivers-architecture"></a>桌面資料庫驅動程式架構
這些驅動程式專為使用在 Microsoft Windows 95 或更新版本，或 Windows NT 4.0 和 Windows 2000。 支援在 Windows 95 或更新版本; 僅限 32 位元應用程式Windows NT 4.0 和 Windows 2000 支援 16 位元和 32 位元應用程式。  
  
> [!NOTE]  
>  如要使用這些驅動程式的 ODBC 版本的相關資訊，請參閱*ODBC 程式設計人員參考*，和過去和目前的版本資訊。 這些驅動程式符合所述的區域，除了*ODBC 程式設計人員參考*。  
  
 ODBC 桌面資料庫驅動程式包含 Microsoft Access、 dBASE、 Microsoft Excel、 Paradox，與文字的 32 位元驅動程式。 無 16 位元驅動程式會包含項目。 （Access 驅動程式是可分開）。  
  
 在 Windows 95 或更新版本的應用程式/驅動程式架構是：  
  
 ![應用程式&#47;驅動程式架構：Windows 95 及更新版本](../../odbc/microsoft/media/odbcjetarch1.gif "ODBCJetArch1")  
  
 不支援這些驅動程式，請在 Windows 95 的 16 位元應用程式使用。  
  
 在 Windows NT 4.0 和 Windows 2000 上的應用程式/驅動程式架構是：  
  
 ![應用程式&#47;驅動程式架構：NT 4.0 和 Windows 2000](../../odbc/microsoft/media/odbcjetarch2.gif "ODBCJetArch2")  
  
 桌面資料庫驅動程式是兩層式驅動程式。 在兩層組態中，驅動程式不會執行剖析、 驗證、 最佳化及執行查詢的程序。 相反地，Microsoft Jet 執行這些工作。 它會處理 ODBC API 呼叫，並可做為 SQL 引擎。 Microsoft Jet 已成為不可或缺，分不開部分驅動程式：它隨附的驅動程式，並位於與驅動程式，即使在電腦上的沒有其他應用程式會使用它。  
  
 桌面資料庫驅動程式包含六個不同的驅動程式-或者，更精確地說，其中一個驅動程式檔案 (Odbcjt32.dll) 的 ODBC[驅動程式管理員](../../odbc/reference/the-driver-manager.md)使用六個不同的方式。 DRIVERID 中的旗標的資料來源的登錄項目會決定 Odbcjt32.dll 中的哪一個驅動程式驅動程式管理員使用。 應用程式會將此旗標傳入的呼叫中所含的連接字串**SQLDriverConnect**。 根據預設，此旗標會是 Microsoft Access 驅動程式的識別碼。  
  
 驅動程式安裝程式檔案會於安裝時期變更 DRIVERID 旗標。 Microsoft Access 驅動程式以外的所有驅動程式會有相關聯的安裝程式 DLL。 當您按一下 **安裝程式**中[Microsoft ODBC 資料來源管理員](../../odbc/admin/odbc-data-source-administrator.md)針對資料來源，ODBC 安裝程式 DLL (Odbcinst.dll) 載入安裝程式 DLL。 安裝程式 DLL 匯出的 ODBC 安裝程式函式**SQLConfigDataSource**。 如果視窗控制代碼傳遞給**SQLConfigDataSource**，此函式會顯示安裝程式視窗，並變更 DRIVERID 旗標，以根據從使用者介面中選取的驅動程式。  
  
 以程式設計方式建立檔案時，要將 NULL 視窗控制代碼傳遞給**SQLConfigDataSource**，和函式會建立資料來源，以動態方式變更 DRIVERID 旗標，根據*lpszDriver*函式呼叫中的引數。  
  
 Odbcjt32.dll 實作 Microsoft Jet API 之上的 ODBC 函數。 不過也 ODBC 和 Microsoft Jet 函式之間沒有直接對應。 許多因素，例如資料指標模型和 SQL 對應，避免直接的相互關聯的函式。  
  
 ODBC 驅動程式位於 Microsoft Jet 引擎和 ODBC 驅動程式管理員之間。 在應用程式呼叫某些 ODBC 函數會處理由驅動程式管理員，並不會傳遞給驅動程式。 這些函式中，Microsoft Jet 永遠看不到函式呼叫，因為它並沒有直接連線至驅動程式管理員。
