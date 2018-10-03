---
title: 使用 16 位元應用程式與 32 位元驅動程式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC drivers [ODBC], 16-bit applications
- 16-bit applications with 32-bit drivers [ODBC]
ms.assetid: 68feb3b7-c01a-4f42-8df9-f9c182d89325
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3ebd6f25758f73e75fd96abb734bc7b0347d5ee0
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47752926"
---
# <a name="using-16-bit-applications-with-32-bit-drivers"></a>搭配使用 16 位元應用程式與 32 位元驅動程式
> [!IMPORTANT]  
>  Windows 的未來版本將移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 請改用 32 位元或 64 位元驅動程式管理員。  
  
 只要 32 位元驅動程式不會明確呼叫建立執行緒的 Win32 API 函式可以在以 Windows 為基礎的系統上執行 32 位元驅動程式 16 位元應用程式。 Windows on Windows (WOW) 子系統上的以 16 位元模式執行的應用程式，並解析 16 位元作業系統的呼叫。 ODBC thunking Dll 解決 16 位元呼叫從 32 位元驅動程式應用程式。 16 位元應用程式使用 Windows API，以及 32 位元驅動程式會使用 Win32 API。  
  
## <a name="architecture"></a>Architecture  
 下圖顯示如何為 16 位元應用程式與 32 位元驅動程式通訊。 16 位元驅動程式管理員之間的 32 位元驅動程式是泛型 thunking 轉換為 32 位元 ODBC 呼叫的 16 位元 ODBC 呼叫的 Dll。  
  
 ![如何 16&#45;位元應用程式與 32 通訊&#45;位元驅動程式](../../odbc/microsoft/media/sdka2.gif "sdka2")  
  
> [!NOTE]  
>  16 位元應用程式與 32 位元驅動程式互動時，每當 32 位元驅動程式管理員一律會傳回"2.0"的 ODBC 版本與驅動程式支援。  
  
## <a name="administration"></a>系統管理  
 您可以使用 ODBC 資料來源管理員來管理資料來源的 32 位元驅動程式。 若要開啟 ODBC 管理員身分執行 Microsoft® Windows® 2000年的電腦上，開啟 Windows 控制台中，按兩下**系統管理工具**，然後按兩下**資料來源 (ODBC)**。 在電腦上執行舊版的 Microsoft Windows，名為圖示**32 位元 ODBC**簡稱**ODBC**。  
  
 下圖顯示的 16 位元應用程式如何呼叫 32 位元驅動程式安裝程式 DLL。 16 位元安裝程式 DLL 與 32 位元驅動程式安裝程式 DLL 會是泛型的 thunk DLL，將轉換的 16 位元安裝程式 DLL 會呼叫 32 位元安裝程式 DLL 呼叫。  
  
 ![如何 16&#45;會呼叫 32 位元應用程式&#45;位元驅動程式安裝 DLL](../../odbc/microsoft/media/sdka3.gif "sdka3")  
  
 在 Windows (thunking 的 16 位元為 32 位元) 上的 Windows，其他的 thunk DLL，名為 Ds32gt.dll 轉換的 16 位元引數值傳遞 32 位元安裝程式 DLL 回 16 位元。  
  
## <a name="components"></a>Components  
 MDAC 2.8 SP1 SDK 的 ODBC 元件包含下列檔案來執行 32 位元驅動程式的 16 位元應用程式。 這些元件是在 \Redist 目錄中。  
  
|[檔案名稱]|描述|  
|---------------|-----------------|  
|Odbc16gt.dll|16 位元 ODBC 泛型 thunk DLL|  
|Odbc32gt.dll|32 位元 ODBC 泛型 thunk DLL|  
|Odbccp32.dll|32 位元安裝程式 DLL|  
|Odbcad32.exe|32 位元系統管理員 」 程式|  
|Odbcinst.hlp|安裝程式說明檔|  
|Ds16gt.dll|泛型 thunking DLL 的 16 位元驅動程式設定|  
|Ctl3d32.dll|32 位元三維的視窗樣式文件庫|  
  
 此外，將下列檔案和 16 位元 ODBC 2.10 驅動程式管理員 中，這不是 ODBC 3.51 的一部分，所需的而且應以 16 位元應用程式安裝。  
  
|[檔案名稱]|描述|  
|---------------|-----------------|  
|Odbc.dll|16 位元驅動程式管理員|  
|Odbcinst.dll|16 位元安裝程式 DLL|  
|Odbcadm.exe|16 位元 ODBC 管理員程式|
