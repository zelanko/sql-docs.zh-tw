---
title: 資料來源的登錄項目 |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: d5f5f865c0b50ea75548bb3a409caef8acf64b51
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47692916"
---
# <a name="registry-entries-for-data-sources"></a>資料來源的登錄項目
> [!NOTE]  
>  從 Windows XP 和 Windows Server 2003 開始，ODBC 會包含在 Windows 作業系統。 您只明確應該安裝在舊版 Windows 上的 ODBC。  
  
 安裝程式 DLL 會維護在登錄中有關每個資料來源的資訊。 在 Microsoft Windows NT/Windows 2000 和 Microsoft Windows 95、windows 98/，這項資訊儲存在其中一個登錄中的下列兩個索引鍵下的子機碼：  
  
 HKEY_LOCAL_MACHINE  
  
 軟體  
  
 ODBC  
  
 Odbc.ini  
  
 HKEY_CURRENT_USER  
  
 軟體  
  
 ODBC  
  
 Odbc.ini  
  
 要使用哪個金鑰取決於資料來源是否*系統資料來源，* 所提供給所有使用者，或有*使用者資料來源，* 即僅適用於目前的使用者。 系統資料來源會儲存在 HKEY_LOCAL_MACHINE 樹狀目錄中，以及使用者資料來源都會儲存在 HKEY_CURRENT_USER 樹狀結構。 在其他方面，系統資料來源和使用者資料來源完全相同的。  
  
 此章節包含下列主題。  
  
-   [ODBC 資料來源子機碼](../../../odbc/reference/install/odbc-data-sources-subkey.md)  
  
-   [資料來源規格子機碼](../../../odbc/reference/install/data-source-specification-subkeys.md)  
  
-   [預設子機碼](../../../odbc/reference/install/default-subkey.md)  
  
-   [ODBC 子機碼](../../../odbc/reference/install/odbc-subkey.md)
