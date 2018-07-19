---
title: 什麼是 ODBC？ | Microsoft Docs
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
- ODBC [ODBC], about ODBC
ms.assetid: badf3a45-f941-44ae-a31d-393116f68a18
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: eed93c1d5b096e132f6d514057abd73c090519c5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32917405"
---
# <a name="what-is-odbc"></a>什麼是 ODBC？
關於 ODBC 許多多疑存在於電腦的世界。 給使用者，它是 Microsoft® Windows® 控制台 中的圖示。 應用程式的程式設計人員，它是包含資料存取常式的程式庫。 許多其他人，所以曾經想像的所有資料庫的存取問題的答案。  
  
 首先和最重要，ODBC 會是資料庫 API 的規格。 這個 API 已獨立於任何一個 DBMS 或作業系統;雖然這份手冊使用 C，ODBC API 是與語言無關。 ODBC API 是以 Open Group 和 ISO/IEC CLI 規格為基礎。 ODBC 3。*x*完全實作這些規格 — 較早版本的 ODBC 已根據這些規格的初步版本，但未完全實作它們，並新增常用的螢幕為基礎的開發人員所需的功能資料庫應用程式，例如可捲動資料指標。  
  
 ODBC API 中的函式是由 DBMS 特定驅動程式的開發人員實作。 應用程式呼叫的函式，在這些驅動程式以存取資料 DBMS 無關的方式。 驅動程式管理員會管理應用程式和驅動程式之間的通訊。  
  
 雖然 Microsoft 提供之執行 Microsoft Windows® 95 的電腦的驅動程式管理員和更新版本中，有數個 ODBC 驅動程式和呼叫 ODBC 函數從寫入某些其應用程式，任何人都可以撰寫 ODBC 應用程式和驅動程式。 事實上，大部分的 ODBC 應用程式和驅動程式目前的寫法是 Microsoft 以外的公司。 此外，ODBC 驅動程式和應用程式存在 Macintosh® 和各種不同的 UNIX 平台上。  
  
 為了協助應用程式和驅動程式的開發人員，Microsoft 提供 ODBC 軟體開發套件 (SDK) 的電腦執行 Windows 95 和更新版本提供的驅動程式管理員，安裝程式 DLL，測試工具和範例應用程式。 Microsoft 已移植這些 Macintosh 和各種不同的 UNIX 平台 Sdk Visigenic 軟體的組合。  
  
 請務必了解 ODBC 設計來公開資料庫功能，不補充它們。 因此，應用程式寫入器不應預期，使用 ODBC 會將突然轉換為簡單資料庫的完整功能的關聯式資料庫引擎。 也不驅動程式寫入器應該實作基礎資料庫中找不到的功能。 這個例外狀況是開發人員撰寫直接存取檔案資料 （例如 Xbase 檔案中的資料） 的驅動程式所需撰寫支援至少要有最小 SQL 功能的資料庫引擎。 另一個例外狀況是 Windows SDK，先前包含在 Microsoft Data Access Components (MDAC) SDK 的 ODBC 元件，可提供模擬的驅動程式實作特定層級的功能，可捲動資料指標的資料指標程式庫。  
  
 使用 ODBC 的應用程式必須負責任何跨資料庫的功能。 例如，ODBC 不是異質性聯結引擎，也不是分散式的交易處理器。 不過，因為它是 DBMS 無關，它可以用來建置這類的跨資料庫工具。
