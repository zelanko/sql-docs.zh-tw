---
title: 資料來源的登錄項目 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- subkeys [ODBC]
- data sources [ODBC], registry entries
- registry entries for data sources [ODBC], about registry entries
- data sources [ODBC], configuring
- registry entries for data sources [ODBC]
ms.assetid: 78aaa3d3-d081-4550-80e3-720c910d5996
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d052b4d64e858837a51a907fc77548bac231c35d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="registry-entries-for-data-sources"></a>資料來源的登錄項目
> [!NOTE]  
>  從 Windows XP 和 Windows Server 2003，ODBC 隨附於 Windows 作業系統。 您只明確應該在舊版 Windows 上安裝 ODBC。  
  
 安裝程式 DLL 維護在登錄中有關每個資料來源的資訊。 在 Microsoft Windows NT/Windows 2000 和 Microsoft Windows 95/98，這項資訊會儲存在登錄中的下列兩個索引鍵的下列其中一個之下的子機碼：  
  
 HKEY_LOCAL_MACHINE  
  
 軟體  
  
 ODBC  
  
 Odbc.ini  
  
 HKEY_CURRENT_USER  
  
 軟體  
  
 ODBC  
  
 Odbc.ini  
  
 要使用哪個金鑰取決於資料來源是否*系統資料來源，*所提供給所有使用者，或*使用者資料來源，*提供到目前的使用者。 系統資料來源上的 HKEY_LOCAL_MACHINE 樹狀目錄中，並儲存使用者資料來源是 HKEY_CURRENT_USER 樹狀目錄上。 在其他方面，系統資料來源和使用者資料來源完全相同。  
  
 此章節包含下列主題。  
  
-   [ODBC 資料來源子機碼](../../../odbc/reference/install/odbc-data-sources-subkey.md)  
  
-   [資料來源規格子機碼](../../../odbc/reference/install/data-source-specification-subkeys.md)  
  
-   [預設子機碼](../../../odbc/reference/install/default-subkey.md)  
  
-   [ODBC 子機碼](../../../odbc/reference/install/odbc-subkey.md)
