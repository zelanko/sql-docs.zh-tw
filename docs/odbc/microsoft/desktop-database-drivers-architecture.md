---
title: 桌面資料庫驅動程式體系結構 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81288738"
---
# <a name="desktop-database-drivers-architecture"></a>桌面資料庫驅動程式架構
這些驅動程式設計用於 Microsoft Windows 95 或更高版本,或 Windows NT 4.0 和 Windows 2000。 Windows 95 或更高版本僅支援 32 位元應用程式;Windows NT 4.0 和 Windows 2000 上支援 16 位元和 32 位元應用程式。  
  
> [!NOTE]  
>  有關要與這些驅動程式一起使用的 ODBC 版本的資訊,請參閱*ODBC 程式師的參考*,以及過去和當前發行說明。 除所述區域外,這些驅動程式符合*ODBC 程式設計師的參考*。  
  
 ODBC 桌面資料庫驅動程式包括用於Microsoft存取、dBASE、微軟Excel、悖論和文本的32位驅動程式。 不包括 16 位驅動程式。 (微軟 FoxPro 的驅動程式單獨提供。  
  
 Windows 95 或更高版本上的應用程式/驅動程式體系結構是:  
  
 ![應用&#47;驅動程式體系結構:Windows 95 及更高版本](../../odbc/microsoft/media/odbcjetarch1.gif "ODBCJetArch1")  
  
 不支援在 Windows 95 上使用 16 位元應用程式使用這些驅動程式。  
  
 Windows NT 4.0 和 Windows 2000 上的應用程式/驅動程式體系結構是:  
  
 ![套用&#47;驅動程式架構結構:NT 4.0 和 Windows 2000](../../odbc/microsoft/media/odbcjetarch2.gif "ODBCJetArch2")  
  
 桌面資料庫驅動程式是雙層驅動程式。 在兩層配置中,驅動程式不執行分析、驗證、優化和執行查詢的過程。 相反,微軟噴氣式飛機執行這些任務。 它處理 ODBC API 呼叫並充當 SQL 引擎。 Microsoft Jet 已經成為驅動程式不可分割的一部分:它與驅動程式一起附帶,並駐留在驅動程式中,即使電腦上沒有其他應用程式使用它。  
  
 桌面資料庫驅動程式由六個不同的驅動程式組成 - 或者更確切地說,一個驅動程式檔 (Odbcjt32.dll),ODBC[驅動程式管理器](../../odbc/reference/the-driver-manager.md)以六種不同的方式使用該檔。 數據源的註冊表條目中的 DRIVERID 標誌確定驅動程式管理器使用的 Odbcjt32.dll 中的哪個驅動程式。 應用程式在**SQLDriverConnect**呼叫中包含的連接字串中傳遞此標誌。 默認情況下,該標誌是Microsoft Access驅動程式的ID。  
  
 驅動程式設定檔在設置時更改 DRIVERID 標誌。 除 Microsoft Access 驅動程式外,所有驅動程式都有關聯的設置 DLL。 當您按下[Microsoft ODBC 資料來源管理員](../../odbc/admin/odbc-data-source-administrator.md)中的 **「設定**」資料來源時,ODBC 安裝程式 DLL (Odbcinst.dll) 將載入安裝程式 DLL。 設定 DLL 匯出 ODBC 安裝程式函數**SQLConfigDataSource**。 如果將視窗句柄傳遞給**SQLConfigDataSource,** 則此功能將顯示一個設定視窗,並根據從使用者介面中選擇的驅動程式更改 DRIVERID 標誌。  
  
 以程式設計方式建立檔時,NULL 視窗句柄將傳遞給**SQLConfigDataSource**,並且函數會動態創建資料來源,根據函數調用中的*lpszDriver*參數更改 DRIVERID 標誌。  
  
 Odbcjt32.dll 在 Microsoft Jet API 之上實現了 ODBC 功能。 但是,ODBC 和 Microsoft Jet 函數之間沒有直接映射。 許多因素(如游標模型和 SQL 映射)阻止函數的直接關聯。  
  
 ODBC 驅動程式位於 Microsoft Jet 引擎和 ODBC 驅動程式管理器之間。 應用程式呼叫的某些 ODBC 函數由驅動程式管理員處理,不會傳遞給驅動程式。 對於這些功能,Microsoft Jet 永遠不會看到函數調用,因為它沒有與驅動程式管理器的直接連接。
