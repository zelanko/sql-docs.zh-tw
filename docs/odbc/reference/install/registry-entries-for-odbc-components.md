---
title: ODBC 元件的登錄項目 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3d0a654b70fb93020bbb0dcfde159b4884cb15c0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63280967"
---
# <a name="registry-entries-for-odbc-components"></a>ODBC 元件的登錄項目
> [!NOTE]  
>  從 Windows XP 和 Windows Server 2003 開始，ODBC 會包含在 Windows 作業系統。 您只明確應該安裝在舊版 Windows 上的 ODBC。  
  
 安裝程式 DLL 會維護在登錄中每個已安裝 ODBC 元件相關的資訊。 在電腦上執行 Microsoft Windows NT 和 Microsoft Windows 95、windows 98/，這項資訊儲存在下列登錄機碼底下的子機碼：  
  
 HKEY_LOCAL_MACHINE  
  
 軟體  
  
 ODBC  
  
 Odbcinst.ini  
  
 Odbcinst.ini 是 HKEY_LOCAL_MACHINE 樹狀結構的子機碼，因為 ODBC 元件的相關資訊可在電腦上的所有使用者。  
  
 此章節包含下列主題。  
  
-   [ODBC 核心子機碼](../../../odbc/reference/install/odbc-core-subkey.md)  
  
-   [ODBC 驅動程式子機碼](../../../odbc/reference/install/odbc-drivers-subkey.md)  
  
-   [驅動程式規格子機碼](../../../odbc/reference/install/driver-specification-subkeys.md)  
  
-   [預設驅動程式子機碼](../../../odbc/reference/install/default-driver-subkey.md)  
  
-   [ODBC 轉譯程式子機碼](../../../odbc/reference/install/odbc-translators-subkey.md)  
  
-   [轉譯程式規格子機碼](../../../odbc/reference/install/translator-specification-subkeys.md)
