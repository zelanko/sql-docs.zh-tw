---
title: 使用 32 位元應用程式與 32 位元驅動程式 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307599"
---
# <a name="using-32-bit-applications-with-32-bit-drivers"></a>搭配使用 32 位元應用程式與 32 位元驅動程式
您可以使用 32 位元驅動程式執行 32 位元應用程式。 32 位元應用程式和 32 位元驅動程式使用 Win32® API。  
  
## <a name="architecture"></a>架構  
 下圖顯示了 32 位元應用程式如何與 32 位驅動程式進行通信。 該應用程式調用 32 位元驅動程式管理員,該管理器又調用 32 位元驅動程式。  
  
 ![32 個&#45;位應用如何與 32 個&#45;位元驅動程式進行通信](../../odbc/microsoft/media/sdka6.gif "sdka6")  
  
> [!IMPORTANT]  
>  請勿在 WindowsNT/Windows2000 上使用 32 位分叉安裝程式 DLL。 儘管它與 32 位安裝程式 DLL 具有相同的檔名,但它是不同的 DLL。  
  
## <a name="administration"></a>系統管理  
 您可以使用 ODBC 資料來源管理員管理 32 位元驅動程式的資料來源。 要在運行 Windows 2000 的電腦上打開 ODBC 管理員,請打開 Windows 控制面板,按兩下**管理工具**,然後按兩下**資料來源 (ODBC)。** 在執行微軟早期版本的 Windows 的電腦上,該圖示被命名為**32 位元 ODBC**或簡稱**ODBC**。  
  
## <a name="components"></a>元件  
 ODBC 元件包括以下檔案,用於使用 32 位元驅動程式運行 32 位元應用程式。 這些元件位於@Redist 目錄中。  
  
|檔案名稱|描述|  
|---------------|-----------------|  
|奧德bc32.dll|32 位元驅動程式管理員|  
|奧德班德32.dll|32 位元安裝程式 DLL|  
|奧德布卡德32.exe|32 位元 ODBC 管理員程式|  
|奧德布金斯特.hlp|安裝程式協助檔案|  
|Msvcrt40.dll|C 執行時庫|
