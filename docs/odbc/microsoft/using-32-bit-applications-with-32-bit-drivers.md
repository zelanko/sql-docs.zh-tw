---
title: 使用32位應用程式搭配32位驅動程式 |Microsoft Docs
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
ms.openlocfilehash: 31512f9339b9d46225bb4f1198cb617a48509acb
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307599"
---
# <a name="using-32-bit-applications-with-32-bit-drivers"></a>搭配使用 32 位元應用程式與 32 位元驅動程式
您可以使用32位驅動程式執行32位應用程式。 32位應用程式和32位驅動程式會使用 Win32® API。  
  
## <a name="architecture"></a>架構  
 下圖顯示32位應用程式如何與32位驅動程式通訊。 應用程式會呼叫32位驅動程式管理員，進而呼叫32位驅動程式。  
  
 ![32&#45;位應用程式如何與 32&#45;位驅動程式通訊](../../odbc/microsoft/media/sdka6.gif "sdka6")  
  
> [!IMPORTANT]  
>  請勿在 WindowsNT/Windows2000 上使用32位的 Thunking 安裝程式 DLL。 雖然它與32位安裝程式 DLL 具有相同的檔案名，但它是不同的 DLL。  
  
## <a name="administration"></a>系統管理  
 您可以使用 [ODBC 資料來源管理員] 來管理32位驅動程式的資料來源。 若要在執行 Windows 2000 的電腦上開啟 ODBC 系統管理員，請開啟 Windows [控制台]，按兩下 [系統**管理工具**]，然後按兩下 **[資料來源（ODBC）**]。 在執行舊版 Microsoft Windows 的電腦上，此圖示的名稱為**32 位 ODBC**或單純的**odbc**。  
  
## <a name="components"></a>元件  
 ODBC 元件包含下列檔案，可執行具有32位驅動程式的32位應用程式。 這些元件位於 \Redist 目錄中。  
  
|檔案名稱|描述|  
|---------------|-----------------|  
|Odbc32.lib .dll|32位驅動程式管理員|  
|Odbccp32 .dll|32位安裝程式 DLL|  
|Odbcad32.exe .exe|32位 ODBC 系統管理員程式|  
|Odbcinst .hlp|安裝程式說明檔|  
|Msvcrt40 .dll|C 執行時間程式庫|
