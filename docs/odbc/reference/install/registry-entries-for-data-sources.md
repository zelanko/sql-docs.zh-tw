---
title: 數據源的註冊表項 |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c73ea704b091bc37afb1ac42b520304022d929c3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296268"
---
# <a name="registry-entries-for-data-sources"></a>資料來源的登錄項目
> [!NOTE]  
>  從 Windows XP 和 Windows 伺服器 2003 開始,ODBC 包含在 Windows 作業系統中。 您只應在早期版本的 Windows 上顯式安裝 ODBC。  
  
 安裝程式 DLL 在註冊表中維護有關每個數據來源的資訊。 在 Microsoft Windows NT/Windows 2000 和 Microsoft Windows 95/98 中,此資訊儲存在註冊表中的以下兩個金鑰之一的子鍵中:  

 ```console
 HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\Odbc.ini  
 ```

 ```console
 HKEY_CURRENT_USER\SOFTWARE\ODBC\Odbc.ini
 ```

 使用哪個金鑰取決於資料來源是*系統資料來源(* 所有使用者都可用)還是*使用者資料來源(* 僅適用於當前使用者)。 系統數據源存儲在HKEY_LOCAL_MACHINE樹上,用戶數據源存儲在HKEY_CURRENT_USER樹上。 在所有其他方面,系統數據源和用戶數據源是相同的。  
  
 此章節包含下列主題。  
  
-   [ODBC 資料來源子機碼](../../../odbc/reference/install/odbc-data-sources-subkey.md)  
  
-   [資料來源規格子機碼](../../../odbc/reference/install/data-source-specification-subkeys.md)  
  
-   [預設子機碼](../../../odbc/reference/install/default-subkey.md)  
  
-   [ODBC 子機碼](../../../odbc/reference/install/odbc-subkey.md)
