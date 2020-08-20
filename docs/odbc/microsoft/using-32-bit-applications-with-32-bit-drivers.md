---
description: 搭配使用 32 位元應用程式與 32 位元驅動程式
title: 使用具有32位驅動程式的32位應用程式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC drivers [ODBC], 32-bit applications
- 32-bit applications with 32-bit drivers [ODBC]
ms.assetid: 0cdd5788-5642-4280-8d53-b4ec461aafa1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 69005071c83047471e76f38160265bc35cdccd4b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471362"
---
# <a name="using-32-bit-applications-with-32-bit-drivers"></a>搭配使用 32 位元應用程式與 32 位元驅動程式
您可以使用32位驅動程式來執行32位應用程式。 32位應用程式和32位驅動程式會使用 Win32® API。  
  
## <a name="architecture"></a>架構  
 下圖顯示32位應用程式如何與32位驅動程式通訊。 應用程式會呼叫32位驅動程式管理員，而後者又會呼叫32位驅動程式。  
  
 ![32&#45;位應用程式如何與 32&#45;位驅動程式通訊](../../odbc/microsoft/media/sdka6.gif "sdka6")  
  
> [!IMPORTANT]  
>  請勿在 WindowsNT/Windows2000 上使用32位 Thunking 安裝程式 DLL。 雖然它的檔案名與32位安裝程式 DLL 相同，但它是不同的 DLL。  
  
## <a name="administration"></a>系統管理  
 您可以使用 [ODBC 資料來源管理員] 來管理32位驅動程式的資料來源。 若要在執行 Windows 2000 的電腦上開啟 ODBC 系統管理員，請開啟 [Windows 主控台，按兩下 [系統 **管理工具**]，然後按兩下 [ **資料來源] ([ODBC) **。 在執行舊版 Microsoft Windows 的電腦上，此圖示名為 **32 位 odbc** 或單純是 **odbc**。  
  
## <a name="components"></a>單元  
 ODBC 元件包含下列檔案，可用於執行具有32位驅動程式的32位應用程式。 這些元件位於 \Redist 目錄中。  
  
|檔案名稱|描述|  
|---------------|-----------------|  
|Odbc32.dll|32位驅動程式管理員|  
|Odbccp32.dll|32位安裝程式 DLL|  
|Odbcad32.exe|32位 ODBC 系統管理員計畫|  
|>odbcinst.ini .hlp|安裝程式說明檔|  
|Msvcrt40.dll|C 執行時間程式庫|
