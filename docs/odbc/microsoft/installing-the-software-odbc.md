---
title: 安裝軟體 (ODBC) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], installing
- installing ODBC driver for Oracle [ODBC]
ms.assetid: dfac8ade-eebe-4ebe-a199-feb740ed5bae
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f3be4f2ce9a3388d53a4d8474e5c1ca172842b5c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68085514"
---
# <a name="installing-the-software-odbc"></a>安裝軟體 (ODBC)
> [!IMPORTANT]  
>  Windows 的未來版本將移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 相反地，使用所提供的 ODBC 驅動程式。  
  
 ODBC Driver for Oracle 是其中一個資料存取元件。 它隨附其他 ODBC 元件，例如 ODBC 資料來源管理員 」 中，應該已經安裝。 驅動程式也可以在 [驅動程式和其他下載] 上找 Microsoft 產品支援服務線上網站在[www.microsoft.com](https://www.microsoft.com)。  
  
 網路軟體必須安裝根據自己的文件。 ODBC Driver for Oracle 需要任何特殊的安裝考量，只要支援的網路軟體。  
  
 根據自己的文件，就必須安裝 oracle 軟體。 ODBC Driver for Oracle，只要此驅動程式支援的版本，通常需要任何特殊的安裝考量。 不過，若要讓產品保持相容，安裝 ODBC Driver for Oracle 上, 一次，以確保您擁有最新版本的驅動程式。 Oracle 會維護公用的 FTP 站台，其中回傳，而在其他方面，Oracle 伺服器產品和用戶端元件的伺服器產品隨附的修補程式。 這些修補程式所需的數個 Microsoft 產品和技術的正常運作。 如需有關此站台的詳細資訊，請參閱[Oracle 軟體修補程式](../../odbc/microsoft/oracle-software-patches.md)。  
  
> [!CAUTION]  
>  透過 MDAC/Windows DAC 安裝 Oracle 軟體，可能會覆寫目前的 MDAC 版本。 如果使用 ODBC 元件發生問題，請重新安裝 MDAC。
