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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bda4abf9802bd58e81f35bd4223b28f687e89b4f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67951790"
---
# <a name="what-is-odbc"></a>什麼是 ODBC？
關於 ODBC 的許多誤解都存在於運算環境中。 對使用者而言，這是 Microsoft® Windows®控制台中的圖示。 對應用程式設計人員來說，它是包含資料存取常式的程式庫。 對許多人來說，這是所有資料庫存取問題的答案。  
  
 首先和最重要的是，ODBC 是資料庫 API 的規格。 此 API 與任何一個 DBMS 或作業系統無關;雖然此手冊使用 C，但 ODBC API 與語言無關。 ODBC API 是以 Open Group 和 ISO/IEC 的 CLI 規格為基礎。 ODBC 3。*x*完全實作為這兩種規格-舊版 ODBC 是根據這些規格的初步版本，但未完全執行，並加入以螢幕為基礎的資料庫應用程式開發人員經常需要的功能，例如可滾動的資料指標。  
  
 ODBC API 中的函式是由 DBMS 特定驅動程式的開發人員所執行。 應用程式會呼叫這些驅動程式中的函數，以 DBMS 獨立的方式存取資料。 驅動程式管理員會管理應用程式和驅動程式之間的通訊。  
  
 雖然 Microsoft 為執行 Microsoft Windows®95和更新版本的電腦提供驅動程式管理員，但已撰寫數個 ODBC 驅動程式，並從它的某些應用程式呼叫 ODBC 函式，但任何人都可以撰寫 ODBC 應用程式和驅動程式。 事實上，現今提供的大部分 ODBC 應用程式和驅動程式都是由 Microsoft 以外的公司所撰寫。 此外，ODBC 驅動程式和應用程式都存在於 Macintosh®和各種 UNIX 平臺上。  
  
 為了協助應用程式和驅動程式開發人員，Microsoft 為執行 Windows 95 和更新版本的電腦提供了 ODBC 軟體發展工具組（SDK），以提供驅動程式管理員、安裝程式 DLL、測試控管和範例應用程式。 Microsoft 結合了 Visigenic Software，將這些 Sdk 移植到 Macintosh 和各種 UNIX 平臺。  
  
 請務必瞭解，ODBC 的設計是要公開資料庫功能，而不是補充它們。 因此，應用程式寫入器應該不會預期使用 ODBC 會突然將簡單的資料庫轉換成功能完整的關係資料庫引擎。 或驅動程式寫入器預期無法執行基礎資料庫中找不到的功能。 唯一的例外是，撰寫直接存取檔案資料的驅動程式（例如 Xbase 檔案中的資料）的開發人員，必須撰寫至少支援最少 SQL 功能的資料庫引擎。 另一個例外狀況是，先前包含在 Microsoft Data Access Components （MDAC） SDK 中的 Windows SDK ODBC 元件會提供資料指標程式庫，以模擬執行特定功能層級之驅動程式的可滾動資料指標。  
  
 使用 ODBC 的應用程式會負責任何跨資料庫的功能。 例如，ODBC 不是異類聯結引擎，也不是分散式交易處理器。 不過，因為它與 DBMS 無關，所以可以用來建立這類跨資料庫工具。
