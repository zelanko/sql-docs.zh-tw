---
description: 什麼是 ODBC？
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
ms.openlocfilehash: 23badedad64ac836f07e3d9f7832fcfa6c33b0b9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88428820"
---
# <a name="what-is-odbc"></a>什麼是 ODBC？
關於 ODBC 的許多誤解都存在於計算世界中。 對終端使用者而言，是 Microsoft® Windows®主控台中的圖示。 對應用程式程式設計人員來說，它是包含資料存取常式的程式庫。 在其他許多情況下，則是所有資料庫存取問題的答案。  
  
 首先也是最重要的是，ODBC 是資料庫 API 的規格。 此 API 與任何一個 DBMS 或作業系統無關;雖然此手動使用 C，但是 ODBC API 與語言無關。 ODBC API 是以開放群組和 ISO/IEC 的 CLI 規格為基礎。 ODBC 3。*x* 完全實行這兩種規格：舊版 ODBC 是以這些規格的初步版本為基礎，但不會完全實行它們，而且會加入以螢幕為基礎的資料庫應用程式開發人員經常需要的功能，例如可滾動的資料指標。  
  
 ODBC API 中的函式是由 DBMS 特定驅動程式的開發人員所執行。 應用程式會呼叫這些驅動程式中的函式，以與 DBMS 無關的方式存取資料。 驅動程式管理員管理應用程式與驅動程式之間的通訊。  
  
 雖然 Microsoft 為執行 Microsoft Windows®95和更新版本的電腦提供了驅動程式管理員，但是已撰寫數個 ODBC 驅動程式，並從其一些應用程式呼叫 ODBC 函數，任何人都可以撰寫 ODBC 應用程式和驅動程式。 事實上，現今可用的大部分 ODBC 應用程式和驅動程式都是由 Microsoft 以外的公司所撰寫。 此外，ODBC 驅動程式和應用程式都存在於 Macintosh®和各種 UNIX 平臺上。  
  
 為了協助應用程式和驅動程式開發人員，Microsoft 為執行 Windows 95 和更新版本的電腦提供了 ODBC 軟體發展工具組 (SDK) ，以提供驅動程式管理員、安裝程式 DLL、測試控管和範例應用程式。 Microsoft 結合了 Visigenic Software，將這些 Sdk 移植到 Macintosh 和各種 UNIX 平臺。  
  
 請務必瞭解，ODBC 是設計來公開資料庫功能，而不是補充它們。 因此，應用程式撰寫者不應預期使用 ODBC 將會突然將簡單的資料庫轉換成功能完整的關係資料庫引擎。 此外，驅動程式寫入器也不會執行在基礎資料庫中找不到的功能。 唯一的例外是，撰寫直接存取檔案 (資料的驅動程式（例如) Xbase 檔中的資料）的開發人員必須撰寫一個支援最低 SQL 功能的資料庫引擎。 另一個例外狀況是 Windows SDK 的 ODBC 元件（先前隨附于 Microsoft Data Access Components (MDAC) SDK）提供了資料指標程式庫，可針對執行特定功能層級的驅動程式，模擬可滾動的資料指標。  
  
 使用 ODBC 的應用程式會負責任何跨資料庫功能。 例如，ODBC 不是異類聯結引擎，也不是分散式交易處理器。 不過，因為它與 DBMS 無關，所以可以用來建立這類的跨資料庫工具。
