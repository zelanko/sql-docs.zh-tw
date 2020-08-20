---
description: 使用計數
title: 使用量計數 |Microsoft Docs
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
ms.openlocfilehash: 8e8c02aae51c47b13970a1824e3c0c9c417eb5f2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499691"
---
# <a name="usage-counting"></a>使用計數
> [!NOTE]  
>  從 Windows XP 和 Windows Server 2003 開始，ODBC 會包含在 Windows 作業系統中。 您應該只在舊版的 Windows 上明確地安裝 ODBC。  
  
 每個元件的登錄中都會保留兩種類型的使用計數：元件使用計數，以及一或多個選用的檔案使用計數。 元件使用計數可協助安裝程式 DLL 維護登錄專案。 它會儲存在 ODBC Core、driver 和 translator 子機碼底下的 UsageCount 值中。 如需 UsageCount 值的格式以及這些子機碼的詳細資訊，請參閱 [ODBC 元件的登錄專案](../../../odbc/reference/install/registry-entries-for-odbc-components.md)。  
  
 第一次安裝元件時，安裝程式 DLL 會為其建立子機碼，並將該子機碼中 UsageCount 值的資料設定為1。 當重新安裝元件時，安裝程式 DLL 會遞增使用計數。 移除元件時，安裝程式 DLL 會遞減使用計數。 如果使用計數降至0，安裝程式 DLL 將會移除元件的子機碼。  
  
> [!CAUTION]  
>  當元件使用計數和檔案使用計數達到零時，應用程式不應該實際移除驅動程式管理員檔案。  
  
 檔案使用計數有助於判斷何時必須實際複製或刪除檔案，而不是遞增或遞減使用計數。 這點很重要，因為 ODBC 元件（以及 ODBC 元件中的檔案）是共用的，而且可以由各種應用程式來安裝或移除。 如果元件使用計數和檔案使用計數達到零，應用程式可以刪除驅動程式和翻譯工具檔案。 不過，當元件使用計數和檔案使用計數都已達到零時，驅動程式管理員檔案不應該刪除，因為這些檔案可供其他尚未遞增檔案使用計數的應用程式使用。  
  
> [!NOTE]  
>  檔案使用計數在 Microsoft® WindowsNT®/Windows2000. 中是選擇性的  
  
 在呼叫 **SQLInstallDriverManager**、 **SQLInstallDriverEx**、 **SQLInstallTranslatorEx**、 **SQLRemoveDriverManager**、 **SQLRemoveDriver**或 **SQLRemoveTranslator**之後，安裝程式會維護檔案使用計數。  
  
 第一次安裝元件時，安裝程式或安裝程式 DLL 會針對該元件中尚未存在於系統上的每個檔案，在下列機碼底下建立一個值：  
  
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
>  Shareddll  
  
 它會將這些值的資料設定為1，並將檔案複製到系統。 再次安裝元件時，安裝程式或安裝程式 DLL 會遞增使用計數。 移除元件時，安裝程式或安裝程式 DLL 會遞減使用計數。 如果任何使用計數降至0，安裝程式或安裝程式 DLL 會移除檔案的值，如果元件是驅動程式或轉譯程式，則會刪除檔案。 驅動程式管理員檔案不應該刪除。  
  
 下表顯示 [檔案使用計數] 值的格式。  
  
|名稱|資料類型|資料|  
|----------|---------------|----------|  
|*完整路徑*|REG_DWORD|*計數*|  
  
 例如，假設 Informix 的驅動程式使用 Infrmx32.dll 和 Infrmx32 的 .hlp 檔案，並假設此驅動程式已安裝兩次。 Informix 驅動程式的 Shareddll 子機碼底下的值如下所示：  
  
```  
C:\WINDOWS\SYSTEM32\INFRMX32.DLL : REG_DWORD : 0x2  
C:\WINDOWS\SYSTEM32\INFRMX32.HLP : REG_DWORD : 0x2  
```
