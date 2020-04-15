---
title: 什麼是 ODBC？ | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC], about ODBC
ms.assetid: badf3a45-f941-44ae-a31d-393116f68a18
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ea0aa81188e5e58d3a66032af38700ece2d4e5b4
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286498"
---
# <a name="what-is-odbc"></a>什麼是 ODBC？
計算領域存在許多關於ODBC的誤解。 對於最終使用者,它是Microsoft ® Windows ®控制面板中的圖示。 對於應用程式程式師來說,它是一個包含數據訪問例程的庫。 對許多其他人來說,這是所有資料庫訪問問題的答案。  
  
 首先,ODBC 是資料庫 API 的規範。 此 API 獨立於任何一個 DBMS 或作業系統;儘管本手冊使用 C,但 ODBC API 與語言無關。 ODBC API 基於開放組和 ISO/IEC 的 CLI 規範。 ODBC 3.*x*完全實現這兩種規範 - 早期版本的 ODBC 基於這些規範的初步版本,但沒有完全實現它們 - 並添加了基於螢幕的資料庫應用程式的開發人員通常需要的功能,例如可滾動的游標。  
  
 ODBC API 中的函數由特定於 DBMS 的驅動程式的開發人員實現。 應用程式呼叫這些驅動程式中的函數以獨立於 DBMS 的方式存取數據。 驅動程式管理員管理應用程式和驅動程式之間的通信。  
  
 儘管 Microsoft 為運行 Microsoft Windows 的電腦提供了驅動程式管理器® 95 及更高版本,但已編寫了多個 ODBC 驅動程式,並從某些應用程式中調用 ODBC 函數,但任何人都可以編寫 ODBC 應用程式和驅動程式。 事實上,目前提供的絕大多數ODBC應用程式和驅動程式是由微軟以外的公司編寫的。 此外,ODBC 的驅動程式和應用程式存在於 Macintosh ®和各種 UNIX 平臺上。  
  
 為了説明應用程式和驅動程式開發人員,Microsoft 為運行 Windows 95 及更高版本的電腦提供了一個 ODBC 軟體開發工具套件 (SDK),該工具套件提供驅動程式管理器、安裝程式 DLL、測試工具和示例應用程式。 微軟與Visigenic軟體公司合作,將這些SDK移植到Macintosh和各種UNIX平臺。  
  
 請務必瞭解,ODBC 旨在公開資料庫功能,而不是補充它們。 因此,應用程式編寫者不應期望使用 ODBC 會突然將簡單資料庫轉換為功能齊全的關係資料庫引擎。 驅動程式編寫器也不期望實現基礎資料庫中找不到的功能。 例外情況是,編寫直接存取檔資料的驅動程式(如 Xbase 檔中的數據)的開發人員需要編寫至少支援最少 SQL 功能的資料庫引擎。 另一個例外是,以前包含在 Microsoft 數據存取元件 (MDAC) SDK 中的 Windows SDK 的 ODBC 元件提供了一個游標庫,用於類比實現特定級別功能的驅動程式的可滾動游標。  
  
 使用 ODBC 的應用程式負責任何跨資料庫功能。 例如,ODBC 不是異構聯接引擎,也不是分散式事務處理器。 但是,由於它與 DBMS 無關,因此可用於構建此類跨資料庫工具。
