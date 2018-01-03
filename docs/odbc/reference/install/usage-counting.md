---
title: "使用方式計數 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- usage counts [ODBC]
- file usage counts [ODBC]
- installing ODBC components [ODBC], usage counts
- subkeys [ODBC], usage counts
ms.assetid: 0678aee9-8256-463c-89dd-77b1a0dfdd60
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: deb6923a2e842241eea1434997194f6e6d19ce1a
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="usage-counting"></a>使用方式計數
> [!NOTE]  
>  從 Windows XP 和 Windows Server 2003，ODBC 隨附於 Windows 作業系統。 您只明確應該在舊版 Windows 上安裝 ODBC。  
  
 每個元件的登錄中維護兩種類型的使用方式計數： 元件使用計數和一或多個選用的檔案使用方式計數。 元件使用計數可幫助的安裝程式 DLL 維護登錄項目。 它會儲存在 ODBC Core、 驅動程式，以及轉譯器的子機碼下的 UsageCount 值。 格式的 UsageCount 值以及這些子機碼的詳細資訊，請參閱[ODBC 元件的登錄項目](../../../odbc/reference/install/registry-entries-for-odbc-components.md)。  
  
 當第一次安裝元件時，安裝程式 DLL 為其建立子機碼與設定 UsageCount 值的資料以子機碼設為 1。 重新安裝元件，安裝程式的 DLL 會遞增的使用計數。 移除元件後，安裝程式 DLL 遞減的使用方式計數。 如果使用計數降至 0，安裝程式的 DLL 會移除元件子機碼。  
  
> [!CAUTION]  
>  當元件使用計數和檔案的使用方式計數達到零，則應用程式應該不實際移除驅動程式管理員的檔案。  
  
 計數協助判斷當檔案必須實際上是複製或刪除的檔案使用相對於遞增或遞減的使用計數。 這是很重要，因為 ODBC 元件，因此 ODBC 元件中的檔案共用，可安裝或移除各種不同的應用程式。 如果元件使用計數和檔案的使用方式計數達到零，應用程式可以刪除驅動程式和轉譯程式檔案。 驅動程式管理員檔案應該不是，不過，刪除時的元件使用計數和檔案使用計數已達到零，因為這些檔案可供其他應用程式，不會遞增檔案使用計數。  
  
> [!NOTE]  
>  檔案的使用方式計數是在 Microsoft® WindowsNT®/為 Windows2000 選擇性的。  
  
 檔案的使用方式計數會維護安裝程式之後，它會呼叫**SQLInstallDriverManager**， **SQLInstallDriverEx**， **SQLInstallTranslatorEx**， **SQLRemoveDriverManager**， **SQLRemoveDriver**，或**SQLRemoveTranslator**。  
  
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
>  以 Shareddll  
  
 它會將這些值的資料設定為 1，並將檔案複製到系統。 重新安裝元件，安裝程式或安裝程式 DLL 遞增使用計數。 移除元件後，安裝程式或安裝程式 DLL 遞減的使用次數。 如果任何使用計數降至 0，安裝程式或 DLL 的安裝程式移除檔案的值，而且如果元件是驅動程式或轉譯器，會刪除檔案。 驅動程式管理員的檔案不應該刪除。  
  
 下表中顯示檔案的使用方式計數值的格式。  
  
|[屬性]|資料類型|data|  
|----------|---------------|----------|  
|*完整路徑*|REG_DWORD|*計數*|  
  
 例如，假設 Informix 的驅動程式會使用 Infrmx32.dll 和 Infrmx32.hlp 檔案，而且假設此驅動程式已安裝兩次。 Informix 驅動程式以 Shareddll 子機碼下的值應如下所示：  
  
```  
C:\WINDOWS\SYSTEM32\INFRMX32.DLL : REG_DWORD : 0x2  
C:\WINDOWS\SYSTEM32\INFRMX32.HLP : REG_DWORD : 0x2  
```
