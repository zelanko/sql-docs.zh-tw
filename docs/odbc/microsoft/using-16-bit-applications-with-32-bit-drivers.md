---
title: 32 位元驅動程式搭配使用 16 位元應用程式 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- ODBC drivers [ODBC], 16-bit applications
- 16-bit applications with 32-bit drivers [ODBC]
ms.assetid: 68feb3b7-c01a-4f42-8df9-f9c182d89325
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d389ada78e2a04b23b046f9a4c1eab8cff736227
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="using-16-bit-applications-with-32-bit-drivers"></a>16 位元應用程式使用 32 位元驅動程式
> [!IMPORTANT]  
>  將移除這項功能，在未來的版本的 Windows。 避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 請改用 32 位元或 64 位元驅動程式管理員。  
  
 32 位元驅動程式不會明確呼叫建立執行緒的 Win32 API 函式時，可以使用 32 位元驅動程式執行 16 位元應用程式在您的 Windows 系統上。 Windows on Windows (WOW) 子系統以 16 位元模式執行的應用程式，並解析 16 位元作業系統的呼叫。 ODBC thunking Dll 解析 16 位元呼叫從 32 位元驅動程式應用程式。 16 位元應用程式使用 Windows API，以及 32 位元驅動程式會使用 Win32 API。  
  
## <a name="architecture"></a>Architecture  
 下圖顯示如何為 16 位元應用程式與 32 位元驅動程式通訊。 16 位元驅動程式管理員之間的 32 位元驅動程式是一般 thunking 轉換為 32 位元 ODBC 呼叫的 16 位元 ODBC 呼叫的 Dll。  
  
 ![如何 16&#45;32 位元應用程式通訊&#45;位元驅動程式](../../odbc/microsoft/media/sdka2.gif "sdka2")  
  
> [!NOTE]  
>  16 位元應用程式與 32 位元驅動程式互動時，每當 32 位元驅動程式管理員一律會傳回"2.0"版本的 ODBC 驅動程式支援。  
  
## <a name="administration"></a>系統管理  
 您可以管理 32 位元驅動程式的資料來源使用 ODBC 資料來源管理員。 若要開啟 ODBC 管理員身分執行 Microsoft® Windows® 2000年的電腦上，開啟 Windows 控制台中，按兩下**系統管理工具**，然後按兩下**資料來源 (ODBC)**。 在電腦上執行舊版 Windows 中，名為圖示**32 位元 ODBC**或只是**ODBC**。  
  
 下圖顯示的 16 位元應用程式如何呼叫 32 位元驅動程式安裝 DLL。 16 位元安裝程式 DLL 之間的 32 位元驅動程式安裝 DLL 會是泛型 thunk DLL，可將轉換的 16 位元安裝程式 DLL 對 32 位元安裝程式 DLL 呼叫的呼叫。  
  
 ![如何 16&#45;位元應用程式會呼叫 32&#45;位元驅動程式安裝 DLL](../../odbc/microsoft/media/sdka3.gif "sdka3")  
  
 在 Windows 上 (thunking 16 位元為 32 位元) 的 Windows 中，名為 Ds32gt.dll 轉換的 16 位元引數值傳遞 32 位元安裝程式的其他 thunk DLL DLL 回 16 位元。  
  
## <a name="components"></a>Components  
 ODBC SDK 元件的 MDAC 2.8 SP1 包含下列 32 位元驅動程式中執行 16 位元應用程式檔案。 這些元件是在 \Redist 目錄中。  
  
|檔案名稱|Description|  
|---------------|-----------------|  
|Odbc16gt.dll|16 位元 ODBC 泛型 thunk DLL|  
|Odbc32gt.dll|32 位元 ODBC 泛型 thunk DLL|  
|Odbccp32.dll|32 位元安裝程式 DLL|  
|Odbcad32.exe|32 位元系統管理員程式|  
|Odbcinst.hlp|安裝程式說明檔|  
|Ds16gt.dll|泛型 thunking DLL 的 16 位元驅動程式安裝程式|  
|Ctl3d32.dll|32 位元三維視窗樣式的文件庫|  
  
 此外，下列的 16 位元 ODBC 2.10 驅動程式管理員，以及檔案不是 ODBC 3.51 的一部分，其所需的而且應該與 16 位元應用程式安裝。  
  
|檔案名稱|Description|  
|---------------|-----------------|  
|Odbc.dll|16 位元驅動程式管理員|  
|Odbcinst.dll|16 位元安裝程式 DLL|  
|Odbcadm.exe|16 位元 ODBC 管理員程式|
