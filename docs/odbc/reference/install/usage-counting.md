---
title: 使用計數 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: edf9976dd3e5d890b46919808e896a8e81a0cd93
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68093796"
---
# <a name="usage-counting"></a>使用計數
> [!NOTE]  
>  從 Windows XP 和 Windows Server 2003 開始，ODBC 會包含在 Windows 作業系統。 您只明確應該安裝在舊版 Windows 上的 ODBC。  
  
 每個元件的登錄中維護兩種類型的使用方式計數： 元件的使用計數和一或多個選用的檔案使用方式計數。 元件使用計數可協助安裝程式 DLL 維護登錄項目。 它會儲存在 ODBC Core、 驅動程式和轉譯程式子機碼之下的 [UsageCount] 值。 格式 UsageCount 值和這些子機碼的詳細資訊，請參閱 < [ODBC 元件的登錄項目](../../../odbc/reference/install/registry-entries-for-odbc-components.md)。  
  
 當第一次安裝元件時，安裝程式 DLL 為其建立子機碼，並設定 UsageCount 值的資料中的子機碼設為 1。 一次安裝元件時，安裝程式 DLL 會遞增的使用計數。 當移除該元件時，安裝程式 DLL 遞減計數使用量。 如果使用計數降至 0，安裝程式 DLL 會移除元件的子機碼。  
  
> [!CAUTION]  
>  當元件使用計數和檔案的使用方式計數到達零，則應用程式應該不實際移除驅動程式管理員的檔案。  
  
 計數協助您判斷當檔案必須實際複製或刪除的檔案使用情況而不是遞增或遞減的使用計數。 這很重要，因為 ODBC 元件，因此 ODBC 元件中的檔案共用，可安裝或移除各種應用程式。 如果元件使用計數和檔案的使用方式計數達到零，應用程式就可以刪除驅動程式，並轉譯程式的檔案。 驅動程式管理員的檔案應該不是，不過，刪除時的元件使用計數和檔案使用計數已達到零，因為這些檔案可供其他應用程式，不會遞增檔案使用計數。  
  
> [!NOTE]  
>  檔案使用方式計數是在 Microsoft® WindowsNT®/Windows2000 選擇性的。  
  
 安裝程式會維護檔案使用方式計數之後它會呼叫, **SQLInstallDriverManager**， **SQLInstallDriverEx**， **SQLInstallTranslatorEx**， **SQLRemoveDriverManager**， **SQLRemoveDriver**，或**SQLRemoveTranslator**。  
  
 當第一次安裝元件時，安裝程式或安裝程式 DLL 會建立每個檔案位於下列機碼值在系統還沒有該元件：  
  
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
>  SharedDlls  
  
 它會將這些值的資料設定為 1，並將檔案複製到系統。 一次安裝元件時，安裝程式或安裝程式 DLL 遞增使用方式計數。 當移除該元件時，安裝程式或安裝程式 DLL 遞減的使用次數。 如果任何使用方式計數降至 0，安裝程式或安裝程式 DLL 移除檔案的值，然後如果元件是驅動程式或轉譯器，會刪除檔案。 應該不會刪除驅動程式管理員的檔案。  
  
 下表中顯示檔案的使用方式計數值的格式。  
  
|名稱|資料類型|Data|  
|----------|---------------|----------|  
|*full-path*|REG_DWORD|*計數*|  
  
 比方說，假設 Informix 的驅動程式會使用 Infrmx32.dll 和 Infrmx32.hlp 檔案，並假設此驅動程式已經安裝了兩次。 Informix 驅動程式以 Shareddll 子機碼下的值應如下所示：  
  
```  
C:\WINDOWS\SYSTEM32\INFRMX32.DLL : REG_DWORD : 0x2  
C:\WINDOWS\SYSTEM32\INFRMX32.HLP : REG_DWORD : 0x2  
```
