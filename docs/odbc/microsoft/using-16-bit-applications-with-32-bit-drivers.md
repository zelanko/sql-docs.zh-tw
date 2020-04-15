---
title: 使用 16 位元應用程式與 32 位元驅動程式 |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c919ed8c3f3791720d67ebdcbf5cfbdbea2a0455
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307629"
---
# <a name="using-16-bit-applications-with-32-bit-drivers"></a>搭配使用 16 位元應用程式與 32 位元驅動程式
> [!IMPORTANT]  
>  此功能將在將來版本的 Windows 中刪除。 避免在新的開發工作中使用此功能,並計劃修改當前使用此功能的應用程式。 改用 32 位元或 64 位元驅動程式管理員。  
  
 只要 32 位元驅動程式不顯式調用建立線程的 Win32 API 函數,就可以在基於 Windows 的系統上運行具有 32 位元驅動程式的 16 位元應用程式。 Windows 上的 Windows (WOW) 子系統以 16 位元模式運行應用程式,並解決對作業系統的 16 位調用。 ODBC thund DLL 解析從應用程式到 32 位元驅動程式的 16 位調用。 16 位元應用程式使用 Windows API,32 位元驅動程式使用 Win32 API。  
  
## <a name="architecture"></a>架構  
 下圖顯示了 16 位應用程式如何與 32 位驅動程式進行通信。 在 16 位元驅動程式管理器和 32 位元驅動程式之間,是通用的 DUN,可將 16 位 ODBC 調用轉換為 32 位 ODBC 調用。  
  
 ![16&#45;位元應用如何與 32 個位驅動程式&#45;位驅動程式進行通訊](../../odbc/microsoft/media/sdka2.gif "sdka2")  
  
> [!NOTE]  
>  每當 16 位元應用程式與 32 位元驅動程式互動時,32 位元驅動程式管理器始終返回「2.0」作為驅動程式支援的 ODBC 版本。  
  
## <a name="administration"></a>系統管理  
 您可以使用 ODBC 資料來源管理員管理 32 位元驅動程式的資料來源。 要在運行 Microsoft ® Windows 的電腦上打開 ODBC 管理員® 2000,請打開 Windows 控制面板,按兩下**管理工具**,然後按兩下**資料來源 (ODBC)。** 在執行微軟早期版本的 Windows 的電腦上,該圖示被命名為**32 位元 ODBC**或簡稱**ODBC**。  
  
 下圖顯示了 16 位元應用程式如何調用 32 位元驅動程式設置 DLL。 在 16 位元安裝程式 DLL 和 32 位元驅動程式設置 DLL 之間,DLL 是一種通用的分接 DLL,可將 16 位元安裝程式 DLL 調用轉換為 32 位元安裝程式 DLL 調用。  
  
 ![16&#45;位元應用如何呼叫 32&#45;位元驅動程式設定 DLL](../../odbc/microsoft/media/sdka3.gif "sdka3")  
  
 在 Windows 上的 Windows(16 位元到 32 位元)中,另一個名為 Ds32gt.dll 的 dLL 將透過 32 位元設定 DLL 傳遞的 16 位元參數值轉換回 16 位元。  
  
## <a name="components"></a>元件  
 MDAC 2.8 SP1 SDK 的 ODBC 元件包括以下檔案,用於運行具有 32 位元驅動程式的 16 位元應用程式。 這些元件位於@Redist 目錄中。  
  
|檔案名稱|描述|  
|---------------|-----------------|  
|奧德bc16gt.dll|16 位元 ODBC 通用分叉 DLL|  
|奧德bc32gt.dll|32 位元 ODBC 通用分叉 DLL|  
|奧德班德32.dll|32 位元安裝程式 DLL|  
|奧德布卡德32.exe|32 位元管理員程式|  
|奧德布金斯特.hlp|安裝程式協助檔案|  
|Ds16gt.dll|16 位元驅動程式設定通用分叉 DLL|  
|Ctl3d32.dll|32 位元 3D 視窗樣式庫|  
  
 此外,以下檔以及 16 位元 ODBC 2.10 驅動程式管理員(不屬於 ODBC 3.51)是必需的,並且應該與 16 位元應用程式一起安裝。  
  
|檔案名稱|描述|  
|---------------|-----------------|  
|奧德布布.dll|16 位元驅動程式管理員|  
|奧德布金斯特.dll|16 位元安裝程式 DLL|  
|奧德布德姆.exe|16 位元 ODBC 管理員程式|
