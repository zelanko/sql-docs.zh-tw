---
title: 使用方式計數 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- usage counts [ODBC]
- file usage counts [ODBC]
- installing ODBC components [ODBC], usage counts
- subkeys [ODBC], usage counts
ms.assetid: 0678aee9-8256-463c-89dd-77b1a0dfdd60
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8d516a591bfde47522c0ccfe08bd2bd706218e07
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296018"
---
# <a name="usage-counting"></a>使用計數
> [!NOTE]  
>  從 Windows XP 和 Windows 伺服器 2003 開始,ODBC 包含在 Windows 作業系統中。 您只應在早期版本的 Windows 上顯式安裝 ODBC。  
  
 每個元件的註冊表中維護兩種類型的使用計數:元件使用計數和一個或多個可選檔使用方式計數。 元件使用計數可説明安裝程式 DLL 維護註冊表項。 它儲存在 ODBC 核心、驅動程式和轉換器子鍵下的「使用方式計數」 值中。 有關使用計數值的格式以及有關這些子鍵的詳細資訊,請參閱[ODBC 元件的註冊表項](../../../odbc/reference/install/registry-entries-for-odbc-components.md)。  
  
 首次安裝元件時,安裝程式 DLL 會為其創建一個子鍵,並將該子鍵中的"使用方式計數"值的數據集到 1。 再次安裝元件時,安裝程式 DLL 會增加使用計數。 刪除元件後,安裝程式 DLL 會減少使用計數。 如果使用計數降至 0,安裝程式 DLL 將刪除元件的子鍵。  
  
> [!CAUTION]  
>  當元件使用計數和檔使用計數達到零時,應用程式不應物理刪除驅動程式管理器檔。  
  
 檔案使用方式計數有助於確定何時必須實際複製或刪除檔,而不是增加或刪除使用計數。 這一點很重要,因為 ODBC 元件以及 ODBC 元件中的檔是共用的,並且可以由各種應用程式安裝或刪除。 如果元件使用計數和檔使用計數達到零,應用程式可以刪除驅動程式和轉換器檔。 但是,當元件使用計數和檔使用計數都達到零時,不應刪除驅動程式管理器檔,因為這些檔可以由未增加檔使用計數的其他應用程式使用。  
  
> [!NOTE]  
>  檔使用方式計數在 Microsoft 中是可選的® WindowsNT ®/Windows2000。  
  
 檔案使用方式計數由安裝程式在調用**SQLInstall 驅動程式管理器****、SQLInstallDriverEx、SQLinstall****翻譯器****、SQLRemove驅動程式管理器****、SQL刪除驅動程式**或**SQLRemove 轉換器**後進行維護。  
  
 設定元件時,安裝程式或安裝程式 DLL 會為該元件中尚未在系統上的每個檔案在以下鍵下建立值:  
  
> [!NOTE]  
>  HKEY_LOCAL_MACHINE  
>   
>  軟體  
>   
>  Microsoft  
>   
>  Windows  
>   
>  CurrentVersion  
>   
>  共用 Dlls  
  
 它將這些值的數據設置為 1,並將檔案複製到系統。 再次安裝元件時,安裝程式或安裝程式 DLL 會增加使用量計數。 刪除元件後,安裝程式或安裝程式 DLL 會減少使用量。 如果任何使用計數降至 0,安裝程式或安裝程式 DLL 將刪除檔案的值,如果元件是驅動程式或轉換器,則刪除該檔。 不應移除驅動程式管理器檔。  
  
 下表顯示了檔使用方式計數值的格式。  
  
|名稱|資料類型|資料|  
|----------|---------------|----------|  
|*全路徑*|REG_DWORD|*count*|  
  
 例如,假設 Informix 的驅動程式使用 Infrmx32.dll 和 Infrmx32.hlp 檔案,並假設此驅動程式已安裝兩次。 Informix 驅動程式的「共用Dll」子鍵下的值如下所示:  
  
```  
C:\WINDOWS\SYSTEM32\INFRMX32.DLL : REG_DWORD : 0x2  
C:\WINDOWS\SYSTEM32\INFRMX32.HLP : REG_DWORD : 0x2  
```
