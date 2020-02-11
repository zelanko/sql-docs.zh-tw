---
title: 安裝軟體（ODBC） |Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68085514"
---
# <a name="installing-the-software-odbc"></a>安裝軟體 (ODBC)
> [!IMPORTANT]  
>  這項功能將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 請改用 Oracle 所提供的 ODBC 驅動程式。  
  
 ODBC Driver for Oracle 是其中一個資料存取元件。 它隨附其他 ODBC 元件，例如 ODBC 資料來源管理員，而且應該已經安裝。 您也可以在 Microsoft 產品支援服務線上網站的 [驅動程式及其他下載] 底下找到此驅動程式，網址為[www.microsoft.com](https://www.microsoft.com)。  
  
 必須根據自己的檔安裝網路軟體。 只要支援網路軟體，ODBC Driver for Oracle 就不需要任何特殊的安裝考慮。  
  
 Oracle 軟體必須根據其本身的檔進行安裝。 ODBC Driver for Oracle 通常不需要任何特殊的安裝考慮，只要驅動程式支援版本即可。 不過，若要讓產品保持相容，請最後安裝 ODBC Driver for Oracle，以確保您擁有最新版本的驅動程式。 Oracle 會維護一個公用 FTP 網站，其中張貼的內容包括 Oracle 伺服器產品的修補程式，以及伺服器產品隨附的用戶端元件。 這些修補程式適用于許多 Microsoft 產品和技術的正常運作。 如需此網站的詳細資訊，請參閱[Oracle 軟體修補程式](../../odbc/microsoft/oracle-software-patches.md)。  
  
> [!CAUTION]  
>  透過 MDAC/Windows DAC 安裝 Oracle 軟體可能會覆寫 MDAC 的最新版本。 如果使用 ODBC 元件發生問題，請重新安裝 MDAC。
