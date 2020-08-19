---
description: 驅動程式安裝程式 DLL
title: 驅動程式安裝程式 DLL |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 79fff6ce68e7860b444ebefa736cb959cd54576b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476204"
---
# <a name="driver-setup-dll"></a>驅動程式安裝程式 DLL
> [!NOTE]  
>  從 Windows XP 和 Windows Server 2003 開始，ODBC 會包含在 Windows 作業系統中。 您應該只在舊版的 Windows 上明確地安裝 ODBC。  
  
 驅動程式安裝程式 DLL 包含 **ConfigDriver** 和 **ConfigDSN** 函數。 **ConfigDriver** 會執行驅動程式特定的安裝工作，例如在登錄中輸入驅動程式特定的資訊。 **ConfigDSN** 會維護有關登錄中資料來源的驅動程式特定資訊。 如需這些功能的完整說明，請參閱 [設定 DLL API 參考](../../../odbc/reference/syntax/setup-dll-api-reference.md)。  
  
 **ConfigDSN** 會在安裝程式 DLL 中呼叫下列函式，以維護登錄中的資料來源資訊：  
  
-   **SQLWriteDSNToIni**。 新增資料來源。  
  
-   **SQLRemoveDSNFromIni**。 刪除資料來源。  
  
-   **SQLWritePrivateProfileString**。 在資料來源規格子機碼底下，寫入驅動程式特定的值。  
  
-   **SQLGetPrivateProfileString**。 從資料來源規格子機碼讀取驅動程式特定的值。  
  
-   **SQLGetTranslator**。 提示使用者輸入 translator 名稱和選項。 此函式會呼叫 translator 安裝程式 DLL 中的 **ConfigTranslator** 。  
  
 驅動程式安裝程式 DLL 是由驅動程式開發人員所撰寫。 它可以是驅動程式 DLL 的一部分或個別的 DLL。
