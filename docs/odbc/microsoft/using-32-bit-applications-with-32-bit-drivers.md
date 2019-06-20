---
title: 使用 32 位元應用程式與 32 位元驅動程式 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5c4f0b21bba9e56cad076ae08f5a561cc972d2ff
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63213469"
---
# <a name="using-32-bit-applications-with-32-bit-drivers"></a>搭配使用 32 位元應用程式與 32 位元驅動程式
您可以執行 32 位元應用程式與 32 位元驅動程式。 32 位元應用程式和 32 位元驅動程式會使用 Win32® API。  
  
## <a name="architecture"></a>Architecture  
 下圖顯示如何為 32 位元應用程式與 32 位元驅動程式通訊。 應用程式會呼叫 32 位元驅動程式管理員，也就會呼叫 32 位元驅動程式。  
  
 ![如何 32&#45;位元應用程式與 32 通訊&#45;位元驅動程式](../../odbc/microsoft/media/sdka6.gif "sdka6")  
  
> [!IMPORTANT]  
>  請勿在 WindowsNT/windows 2000 上使用 32 位元 thunk 安裝程式 DLL。 雖然有相同的檔案名稱，因為 32 位元安裝程式 DLL，它會是不同的 DLL。  
  
## <a name="administration"></a>系統管理  
 您可以使用 ODBC 資料來源管理員來管理資料來源的 32 位元驅動程式。 若要開啟 ODBC 管理員，在執行 Windows 2000 的電腦上，開啟 Windows 控制台中，按兩下**系統管理工具**，然後按兩下**資料來源 (ODBC)** 。 在電腦上執行舊版的 Microsoft Windows，名為圖示**32 位元 ODBC**簡稱**ODBC**。  
  
## <a name="components"></a>元件  
 ODBC 元件包含下列檔案來執行 32 位元驅動程式的 32 位元應用程式。 這些元件是在 \Redist 目錄中。  
  
|[檔案名稱]|描述|  
|---------------|-----------------|  
|Odbc32.dll|32 位元驅動程式管理員|  
|Odbccp32.dll|32 位元安裝程式 DLL|  
|Odbcad32.exe|32 位元 ODBC 管理員程式|  
|Odbcinst.hlp|安裝程式說明檔|  
|Msvcrt40.dll|C 執行階段程式庫|
