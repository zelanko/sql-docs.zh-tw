---
title: 資料來源的登錄專案 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- subkeys [ODBC]
- data sources [ODBC], registry entries
- registry entries for data sources [ODBC], about registry entries
- data sources [ODBC], configuring
- registry entries for data sources [ODBC]
ms.assetid: 78aaa3d3-d081-4550-80e3-720c910d5996
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1fe76ba3926f2883e2518e255eddf0d567134f4d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "70009351"
---
# <a name="registry-entries-for-data-sources"></a>資料來源的登錄項目
> [!NOTE]  
>  從 Windows XP 和 Windows Server 2003 開始，ODBC 包含在 Windows 作業系統中。 您只應該在舊版 Windows 上明確安裝 ODBC。  
  
 安裝程式 DLL 會在登錄中維護每個資料來源的相關資訊。 在 Microsoft Windows NT/Windows 2000 和 Microsoft Windows 95/98 中，這項資訊會儲存在登錄中下列兩個金鑰之一底下的子機碼中：  

 ```console
 HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\Odbc.ini  
 ```

 ```console
 HKEY_CURRENT_USER\SOFTWARE\ODBC\Odbc.ini
 ```

 使用哪個索引鍵取決於資料來源是否為*系統資料來源（* 可供所有使用者使用），或是僅供目前使用者使用的*使用者資料來源*。 系統資料來源會儲存在 HKEY_LOCAL_MACHINE 樹狀目錄上，而使用者資料來源會儲存在 HKEY_CURRENT_USER 樹狀目錄上。 在所有其他方面，系統資料來源和使用者資料來源都相同。  
  
 此章節包含下列主題。  
  
-   [ODBC 資料來源子機碼](../../../odbc/reference/install/odbc-data-sources-subkey.md)  
  
-   [資料來源規格子機碼](../../../odbc/reference/install/data-source-specification-subkeys.md)  
  
-   [預設子機碼](../../../odbc/reference/install/default-subkey.md)  
  
-   [ODBC 子機碼](../../../odbc/reference/install/odbc-subkey.md)
