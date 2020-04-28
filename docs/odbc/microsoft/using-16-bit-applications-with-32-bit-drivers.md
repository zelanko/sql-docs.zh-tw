---
title: 搭配使用16位應用程式與32位驅動程式 |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307629"
---
# <a name="using-16-bit-applications-with-32-bit-drivers"></a>搭配使用 16 位元應用程式與 32 位元驅動程式
> [!IMPORTANT]  
>  這項功能將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 請改用32位或64位驅動程式管理員。  
  
 只要32位驅動程式未明確呼叫建立執行緒的 WIN32 API 函式，您就可以在 Windows 系統上執行具有32位驅動程式的16位應用程式。 Windows on Windows （WOW）子系統會在16位模式中執行應用程式，並將16位呼叫解析為作業系統。 ODBC Thunking Dll 可將應用程式的16位呼叫解析為32位驅動程式。 16位應用程式會使用 Windows API，而32位驅動程式會使用 WIN32 API。  
  
## <a name="architecture"></a>架構  
 下圖顯示16位應用程式如何與32位驅動程式通訊。 在16位驅動程式管理員和32位驅動程式之間，是將16位 ODBC 呼叫轉換成32位 ODBC 呼叫的一般 Thunking Dll。  
  
 ![16個&#45;位應用程式如何與 32&#45;位驅動程式通訊](../../odbc/microsoft/media/sdka2.gif "sdka2")  
  
> [!NOTE]  
>  每當16位應用程式與32位驅動程式互動時，32位驅動程式管理員一律會傳回 "2.0" 做為驅動程式所支援的 ODBC 版本。  
  
## <a name="administration"></a>系統管理  
 您可以使用 [ODBC 資料來源管理員] 來管理32位驅動程式的資料來源。 若要在執行 Microsoft® Windows®2000的電腦上開啟 ODBC 系統管理員，請開啟 Windows [控制台]，按兩下 [系統**管理工具**]，然後按兩下 **[資料來源（ODBC）**]。 在執行舊版 Microsoft Windows 的電腦上，此圖示的名稱為**32 位 ODBC**或單純的**odbc**。  
  
 下圖顯示16位應用程式如何呼叫32位驅動程式安裝 DLL。 在16位安裝程式 DLL 和32位驅動程式安裝程式 DLL 之間，是將16位安裝程式 DLL 呼叫轉換成32位安裝程式 DLL 呼叫的一般 Thunking DLL。  
  
 ![16&#45;位應用程式如何呼叫 32&#45;位驅動程式安裝 DLL](../../odbc/microsoft/media/sdka3.gif "sdka3")  
  
 在 windows on Windows （16位到32位的 Thunking）中，名為 Ds32gt 的其他 Thunking DLL 會將透過32位安裝 DLL 傳遞的16位引數值轉換回16位。  
  
## <a name="components"></a>元件  
 MDAC 2.8 SP1 SDK 的 ODBC 元件包含下列檔案，可執行具有32位驅動程式的16位應用程式。 這些元件位於 \Redist 目錄中。  
  
|檔案名稱|描述|  
|---------------|-----------------|  
|Odbc16gt .dll|16位 ODBC 泛型 Thunking DLL|  
|Odbc32gt .dll|32位 ODBC 泛型 Thunking DLL|  
|Odbccp32 .dll|32位安裝程式 DLL|  
|Odbcad32.exe .exe|32位系統管理員程式|  
|Odbcinst .hlp|安裝程式說明檔|  
|Ds16gt .dll|16位驅動程式安裝程式一般 Thunking DLL|  
|Ctl3d32 .dll|32位三維視窗樣式程式庫|  
  
 此外，下列檔案以及不屬於 ODBC 3.51 的16位 ODBC 2.10 驅動程式管理員，都是必要的，而且應該與16位應用程式一起安裝。  
  
|檔案名稱|描述|  
|---------------|-----------------|  
|Odbc .dll|16位驅動程式管理員|  
|Odbcinst .dll|16位安裝程式 DLL|  
|Odbcadm .exe|16位 ODBC 系統管理員程式|
