---
title: "驅動程式安裝 DLL |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- installing ODBC components [ODBC], driver setup DLL
- ODBC drivers [ODBC], driver setup DLL
- driver setup DLL [ODBC]
ms.assetid: 49bab021-81fa-402e-b7a4-a5214f1fadc4
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d75a8985feff2ddfe26d3e19e8bafd91f228d30e
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="driver-setup-dll"></a>驅動程式安裝 DLL
> [!NOTE]  
>  從 Windows XP 和 Windows Server 2003，ODBC 隨附於 Windows 作業系統。 您只明確應該在舊版 Windows 上安裝 ODBC。  
  
 驅動程式安裝程式 DLL 包含**ConfigDriver**和**ConfigDSN**函式。 **ConfigDriver**執行特定驅動程式安裝工作，例如在登錄中輸入驅動程式特有的資訊。 **ConfigDSN**維護在登錄中的資料來源的驅動程式特定資訊。 如需這些函式的完整說明，請參閱[安裝 DLL 應用程式開發介面參考](../../../odbc/reference/syntax/setup-dll-api-reference.md)。  
  
 **ConfigDSN**在安裝程式維護在登錄中的資料來源資訊的 DLL 呼叫下列函數：  
  
-   **SQLWriteDSNToIni**。 加入資料來源。  
  
-   **SQLRemoveDSNFromIni**。 刪除資料來源。  
  
-   **SQLWritePrivateProfileString**。 寫入資料來源規格子機碼下的驅動程式專屬值。  
  
-   **SQLGetPrivateProfileString**。 從資料來源規格子機碼讀取驅動程式專屬值。  
  
-   **SQLGetTranslator**。 提示使用者輸入的轉譯程式名稱和選項。 此函數會呼叫**ConfigTranslator**轉譯程式中安裝的 DLL。  
  
 驅動程式安裝程式的 DLL 是由驅動程式開發人員撰寫。 它可以是一部分的驅動程式 DLL 或個別的 DLL。

