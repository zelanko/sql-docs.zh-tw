---
title: "ODBC 元件的登錄項目 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- subkeys [ODBC]
- installing ODBC components [ODBC], registry entries
- registry entries for components [ODBC]
- subkeys [ODBC], for components
- registry entries for components [ODBC], about registry entries
ms.assetid: c90aa8a4-6ece-48de-901c-17d23739a9ff
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: f32934e96948ad9b2fa7e9359437106b43464e65
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="registry-entries-for-odbc-components"></a>ODBC 元件的登錄項目
> [!NOTE]  
>  從 Windows XP 和 Windows Server 2003，ODBC 隨附於 Windows 作業系統。 您只明確應該在舊版 Windows 上安裝 ODBC。  
  
 安裝程式的 DLL 會維護在登錄中每個已安裝的 ODBC 元件相關的資訊。 在電腦上執行 Microsoft Windows NT 和 Microsoft Windows 95/98，這項資訊會儲存在下列登錄機碼下的子機碼：  
  
 HKEY_LOCAL_MACHINE  
  
 軟體  
  
 ODBC  
  
 Odbcinst.ini  
  
 Odbcinst.ini 是 HKEY_LOCAL_MACHINE 樹狀結構的子機碼，因為 ODBC 元件的相關資訊是供所有使用者的電腦。  
  
 此章節包含下列主題。  
  
-   [ODBC 核心子機碼](../../../odbc/reference/install/odbc-core-subkey.md)  
  
-   [ODBC 驅動程式子機碼](../../../odbc/reference/install/odbc-drivers-subkey.md)  
  
-   [驅動程式規格子機碼](../../../odbc/reference/install/driver-specification-subkeys.md)  
  
-   [預設驅動程式子機碼](../../../odbc/reference/install/default-driver-subkey.md)  
  
-   [ODBC 轉譯程式子機碼](../../../odbc/reference/install/odbc-translators-subkey.md)  
  
-   [轉譯程式規格子機碼](../../../odbc/reference/install/translator-specification-subkeys.md)
