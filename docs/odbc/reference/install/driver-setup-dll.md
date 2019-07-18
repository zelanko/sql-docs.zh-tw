---
title: 驅動程式安裝 DLL |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- installing ODBC components [ODBC], driver setup DLL
- ODBC drivers [ODBC], driver setup DLL
- driver setup DLL [ODBC]
ms.assetid: 49bab021-81fa-402e-b7a4-a5214f1fadc4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: df91638f91091940e00e7a6a19d0fd6cb700f85f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68094166"
---
# <a name="driver-setup-dll"></a>驅動程式安裝程式 DLL
> [!NOTE]  
>  從 Windows XP 和 Windows Server 2003 開始，ODBC 會包含在 Windows 作業系統。 您只明確應該安裝在舊版 Windows 上的 ODBC。  
  
 驅動程式安裝程式 DLL 包含**ConfigDriver**並**ConfigDSN**函式。 **ConfigDriver**會執行特定驅動程式安裝工作，例如在登錄中輸入驅動程式特有的資訊。 **ConfigDSN**會保存在登錄中的資料來源的驅動程式特定資訊。 如需這些函式的完整說明，請參閱 <<c0> [ 安裝程式 DLL API 參考](../../../odbc/reference/syntax/setup-dll-api-reference.md)。  
  
 **ConfigDSN**在安裝程式中維護在登錄中的資料來源資訊的 DLL 呼叫下列函數：  
  
-   **SQLWriteDSNToIni**。 新增資料來源。  
  
-   **SQLRemoveDSNFromIni**。 刪除資料來源。  
  
-   **SQLWritePrivateProfileString**。 寫入資料來源規格子機碼下的驅動程式專屬值。  
  
-   **SQLGetPrivateProfileString**。 讀取的資料來源規格子機碼中的驅動程式專屬值。  
  
-   **SQLGetTranslator**。 提示使用者輸入的轉譯器名稱和選項。 此函式會呼叫**ConfigTranslator**轉譯程式中安裝 DLL。  
  
 驅動程式安裝程式 DLL 是由驅動程式開發人員撰寫。 它可以是在驅動程式 DLL 或不同的 DLL。
