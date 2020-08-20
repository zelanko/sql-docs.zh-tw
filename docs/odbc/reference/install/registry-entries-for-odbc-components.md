---
description: ODBC 元件的登錄項目
title: ODBC 元件的登錄專案 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- subkeys [ODBC]
- installing ODBC components [ODBC], registry entries
- registry entries for components [ODBC]
- subkeys [ODBC], for components
- registry entries for components [ODBC], about registry entries
ms.assetid: c90aa8a4-6ece-48de-901c-17d23739a9ff
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e3364f2b38fdb0c41ae0493b545740b17ee712bf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88491333"
---
# <a name="registry-entries-for-odbc-components"></a>ODBC 元件的登錄項目
> [!NOTE]  
>  從 Windows XP 和 Windows Server 2003 開始，ODBC 會包含在 Windows 作業系統中。 您應該只在舊版的 Windows 上明確地安裝 ODBC。  
  
 安裝程式 DLL 會在登錄中維護每個已安裝 ODBC 元件的相關資訊。 在執行 Microsoft Windows NT 和 Microsoft Windows 95/98 的電腦上，此資訊會儲存在登錄中下列機碼下的子機碼中：  

 ```console
 HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\Odbcinst.ini
 ```

 因為 Odbcinst.ini 是 HKEY_LOCAL_MACHINE 樹狀目錄的子機碼，所以電腦的所有使用者都可以使用 ODBC 元件的相關資訊。  
  
 此章節包含下列主題。  
  
-   [ODBC 核心子機碼](../../../odbc/reference/install/odbc-core-subkey.md)  
  
-   [ODBC 驅動程式子機碼](../../../odbc/reference/install/odbc-drivers-subkey.md)  
  
-   [驅動程式規格子機碼](../../../odbc/reference/install/driver-specification-subkeys.md)  
  
-   [預設驅動程式子機碼](../../../odbc/reference/install/default-driver-subkey.md)  
  
-   [ODBC 轉譯程式子機碼](../../../odbc/reference/install/odbc-translators-subkey.md)  
  
-   [轉譯程式規格子機碼](../../../odbc/reference/install/translator-specification-subkeys.md)
