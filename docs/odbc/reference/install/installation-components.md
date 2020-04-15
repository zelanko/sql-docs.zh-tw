---
title: 安裝元件 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- installing ODBC components [ODBC], setup program
- ODBC [ODBC], component installation
ms.assetid: 9de15ca0-fe6a-4634-8709-a928d3c9cc73
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0a196e9b935229fa03c6dd0eda92b8e99e69f0ca
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285248"
---
# <a name="installation-components"></a>安裝元件
> [!NOTE]  
>  從 Windows XP 和 Windows 伺服器 2003 開始,ODBC 包含在 Windows 作業系統中。 您只應在早期版本的 Windows 上顯式安裝 ODBC。  
  
 當使用者運行安裝程式時,安裝過程將啟動。 安裝程式與*安裝程式 DLL*和每個*驅動程式的驅動程式設置 DLL*結合使用。 安裝程式和安裝程式 DLL 都使用**SQLInstallDriverEx**和**SQLInstallTranslatorEx**函數中的參數來確定要為每個元件複製或刪除哪些檔。 下圖顯示了這些安裝元件之間的關係。  
  
 ![安裝元件間的關聯性](../../../odbc/reference/install/media/pr29.gif "pr29")  
  
> [!IMPORTANT]
>  ODBC.inf 檔案在 ODBC *2.x*中用於描述每個 ODBC 元件所需的檔案,在 ODBC *3.x*中不使用。 提供 ODBC *3.x*元件的驅動程式不需要創建 Odbc.inf 檔案。 **SQLInstallDriver**和**SQLInstallODBC**的刪除,以及**SQLInstall 轉換器**的棄用,使得 Odbc.inf 變得沒有必要。 以前位於 Odbc.inf 的驅動程式關鍵字部分中的驅動程式資訊現在在**SQLInstallDriverEx**中的*lpszDriver*參數中提供。 以前位於 Odbc.inf 的 [ODBC 轉換器] 和翻譯器規範部分的轉換器資訊現在在**SQLinstall 翻譯器 Ex**的*lpsz 轉換器*參數中提供。 這些更改使 ODBC 安裝程式在跨平臺中更加便攜。  
  
 有關這些元件的詳細資訊,請參閱本節末尾的以下主題。  
  
-   [安裝程式](../../../odbc/reference/install/setup-program.md)  
  
-   [安裝程式 DLL](../../../odbc/reference/install/installer-dll.md)  
  
-   [驅動程式安裝程式 DLL](../../../odbc/reference/install/driver-setup-dll.md)
