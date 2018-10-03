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
manager: craigg
ms.openlocfilehash: 27e153fd72c588f81342d74ce1fc851adc6fda91
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47622326"
---
# <a name="what-is-odbc"></a>什麼是 ODBC？
ODBC 的許多誤解存在於運算的世界。 給使用者，它是 Microsoft® Windows® 控制台 中的圖示。 應用程式的程式設計人員，它是包含資料存取常式的程式庫。 若要多人就曾經假設所有資料庫的存取問題的答案。  
  
 首先，ODBC 會是資料庫 API 的規格。 此 API 是獨立於任何一個 DBMS 或作業系統;雖然本手冊會使用 C，ODBC API 是與語言無關。 ODBC API 是以 Open Group 和 ISO/IEC CLI 規格為基礎。 ODBC 3。*x*完全實作這些規格 — 較早版本的 ODBC 已根據這些規格的初步版本，但未完整實作它們，並新增功能，通常需要由螢幕為基礎的開發人員資料庫應用程式，例如可捲動資料指標。  
  
 ODBC API 中的函式的實作方式的 DBMS 特定驅動程式的開發人員。 應用程式會呼叫函式，在這些驅動程式以存取資料的 DBMS 無關的方式。 驅動程式管理員會管理應用程式和驅動程式之間的通訊。  
  
 雖然 Microsoft 會提供執行 Microsoft Windows® 95 的電腦上的驅動程式管理員，並更新版本中，有數個 ODBC 驅動程式和呼叫 ODBC 函數從寫入某些應用程式，任何人都可以撰寫 ODBC 應用程式和驅動程式。 事實上，絕大多數的 ODBC 應用程式和驅動程式提供立即的寫法是 Microsoft 以外的公司。 此外，ODBC 驅動程式和應用程式存在 Macintosh® 和各種不同的 UNIX 平台上。  
  
 為了協助應用程式和驅動程式的開發人員，Microsoft 提供 ODBC 軟體開發套件 (SDK) 的電腦執行 Windows 95 和更新版本所提供的驅動程式管理員，安裝程式 DLL，測試工具和範例應用程式。 Microsoft 已移植到 Macintosh 與各種不同的 UNIX 平台 Sdk 的 Visigenic 軟體組合。  
  
 請務必了解 ODBC 會公開 （expose） 的資料庫功能，不補充它們設計。 因此，應用程式寫入器不應預期，使用 ODBC 會突然將轉換的簡單資料庫的完整功能的關聯式資料庫引擎。 也會驅動程式撰寫者必須實作基礎資料庫中找不到的功能。 這個例外狀況是撰寫直接存取檔案資料 （例如 Xbase 檔案中的資料） 的驅動程式的開發人員必須撰寫支援至少最基本的 SQL 功能的資料庫引擎。 另一個例外狀況是 Windows SDK 中，原本是收錄在 Microsoft Data Access Components (MDAC) SDK 的 ODBC 元件，並提供資料指標程式庫，以模擬可捲動資料指標的驅動程式，實作某種程度的功能。  
  
 使用 ODBC 的應用程式會負責任何跨資料庫功能。 比方說，ODBC 不是異質性聯結引擎，也不是分散式的交易處理器。 不過，因為它是 DBMS 無關，它可以用來建置這類跨資料庫的工具。
