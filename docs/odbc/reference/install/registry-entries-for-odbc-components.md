---
title: ODBC 元件的註冊表項 |微軟文件
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
ms.openlocfilehash: bead63f11b253342cd444e1d5bd0697ee00cfbc1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296168"
---
# <a name="registry-entries-for-odbc-components"></a>ODBC 元件的登錄項目
> [!NOTE]  
>  從 Windows XP 和 Windows 伺服器 2003 開始,ODBC 包含在 Windows 作業系統中。 您只應在早期版本的 Windows 上顯式安裝 ODBC。  
  
 安裝程式 DLL 在註冊表中維護有關每個已安裝的 ODBC 元件的資訊。 在執行 Microsoft Windows NT 和 Microsoft Windows 95/98 的電腦上,此資訊儲存在註冊表中的以下鍵下的子金鑰中:  

 ```console
 HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\Odbcinst.ini
 ```

 由於 Odbcinst.ini 是HKEY_LOCAL_MACHINE樹的子鍵,因此有關 ODBC 元件的資訊可供機器的所有使用者使用。  
  
 此章節包含下列主題。  
  
-   [ODBC 核心子機碼](../../../odbc/reference/install/odbc-core-subkey.md)  
  
-   [ODBC 驅動程式子機碼](../../../odbc/reference/install/odbc-drivers-subkey.md)  
  
-   [驅動程式規格子機碼](../../../odbc/reference/install/driver-specification-subkeys.md)  
  
-   [預設驅動程式子機碼](../../../odbc/reference/install/default-driver-subkey.md)  
  
-   [ODBC 轉譯程式子機碼](../../../odbc/reference/install/odbc-translators-subkey.md)  
  
-   [轉譯程式規格子機碼](../../../odbc/reference/install/translator-specification-subkeys.md)
