---
title: 管理計劃 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- administration program [ODBC]
- ODBC administrator [ODBC]
ms.assetid: a6c8248a-7a01-42e7-aaed-99dc94d50028
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d8a2a8363371d6f6c3644c2b7b49aa77644d496e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306639"
---
# <a name="administration-program"></a>管理程式
> [!NOTE]  
>  從 Windows XP 和 Windows 伺服器 2003 開始,ODBC 包含在 Windows 作業系統中。 您只應在早期版本的 Windows 上顯式安裝 ODBC。  
  
 Windows SDK/MDAC SDK 中包括一個管理程式(ODBC 管理員)。 此程式,並且可以由 SDK 的使用者重新分發。 此外,開發人員可以編寫自己的管理程式。 通常,開發人員只有在希望保留對數據源配置的完全控制時,或者直接從充當管理程式的應用程序配置數據源時,才編寫自己的管理程式。 例如,電子表格程式可能允許使用者在運行時添加和使用數據源。  
  
 管理程式首先載入安裝程式 DLL。 然後,呼叫安裝程式 DLL 中的函數以執行以下工作:  
  
-   **以互動方式添加、修改或刪除資料來源。** 管理程式可以呼叫**SQLManageDataSource、SQLCreate****資料來源**或**SQLConfigDataSource**。  
  
     **SQLManageDataSources**顯示一個對話框,用戶可以用該對話方塊添加、修改或刪除數據源並指定跟蹤選項;當直接從控制面板調用安裝程式 DLL 時,將調用此功能。 **SQLCreateDataSource**顯示一個對話框,使用者可以使用該對話框添加數據源。 **SQLConfigDataSource**將呼叫直接傳遞到驅動程式設置 DLL。  
  
     在所有情況下,安裝程式 DLL 在驅動程式設置 DLL 中調用**ConfigDSN**以實際添加、修改或刪除資料來源。 驅動程式設置 DLL 可能會提示使用者以獲取其他資訊。  
  
-   **靜默添加、修改或刪除資料源。** 管理程式在安裝程式 DLL 中呼叫**SQLConfigDataSource,** 並傳遞一個空視窗句柄、要添加、修改或刪除的資料來源的名稱以及註冊表的值清單。 安裝程式 DLL 在驅動程式設定 DLL 中呼叫**ConfigDSN**以實際新增、修改或刪除資料來源。  
  
-   **新增、修改或刪除預設資料來源。** 默認數據源與任何其他數據源相同,只不過其名稱為"預設"。 它以與任何其他數據源相同的方式添加、修改或刪除。
