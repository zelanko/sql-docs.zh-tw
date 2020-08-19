---
description: 安裝軟體 (ODBC)
title: " (ODBC) 安裝軟體 |Microsoft Docs"
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fe161ef45ef91f67317d7a0b465e00d3d2045c40
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449470"
---
# <a name="installing-the-software-odbc"></a>安裝軟體 (ODBC)
> [!IMPORTANT]  
>  未來的 Windows 版本將會移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 請改用 Oracle 提供的 ODBC 驅動程式。  
  
 ODBC Driver for Oracle 是其中一個資料存取元件。 它隨附其他 ODBC 元件，例如 ODBC 資料來源系統管理員，而且應該已經安裝。 您也可以在 Microsoft 產品支援服務線上網站的「驅動程式和其他下載」下找到此驅動程式，網址為 [www.microsoft.com](https://www.microsoft.com)。  
  
 網路軟體必須根據其本身的檔進行安裝。 只要支援網路軟體，ODBC Driver for Oracle 不需要任何特殊的安裝考慮。  
  
 Oracle 軟體必須根據自己的檔進行安裝。 ODBC Driver for Oracle 通常不需要任何特殊的安裝考慮，只要驅動程式支援版本即可。 不過，若要保持產品的相容性，請先安裝 ODBC Driver for Oracle，以確保您擁有最新版本的驅動程式。 Oracle 會維護一個公用 FTP 網站，其中包含與伺服器產品一起發行的 Oracle server 產品和用戶端元件的修補程式。 需要這些修補程式才能正常運作數種 Microsoft 產品和技術。 如需此網站的詳細資訊，請參閱 [Oracle 軟體修補程式](../../odbc/microsoft/oracle-software-patches.md)。  
  
> [!CAUTION]  
>  透過 MDAC/Windows DAC 安裝 Oracle 軟體可能會覆寫 MDAC 的最新版本。 如果使用 ODBC 元件發生問題，請重新安裝 MDAC。
