---
title: 安裝軟體 (ODBC) |微軟文件
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
ms.openlocfilehash: 9bddfd9947017cc94214e57948e495b06cccc1cb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299978"
---
# <a name="installing-the-software-odbc"></a>安裝軟體 (ODBC)
> [!IMPORTANT]  
>  此功能將在將來版本的 Windows 中刪除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 而是使用 Oracle 提供的 ODBC 驅動程式。  
  
 Oracle 的 ODBC 驅動程式是數據存取元件之一。 它附帶其他 ODBC 元件,如 ODBC 數據源管理員,並且應該已經安裝。 該驅動程式也可以在微軟產品支援服務在線網站上找到[www.microsoft.com](https://www.microsoft.com)下的「驅動程式和其他下載」。  
  
 網路軟體必須根據自己的文檔進行安裝。 Oracle 的 ODBC 驅動程式不需要特殊的安裝注意事項,只要支援網路軟體。  
  
 Oracle 軟體必須根據自己的文檔進行安裝。 Oracle 的 ODBC 驅動程式通常不需要特殊的安裝注意事項,只要驅動程式支援該版本。 但是,要保持產品相容,請最後安裝 Oracle 的 ODBC 驅動程式,以確保您擁有最新版本的驅動程式。 Oracle 維護一個公共 FTP 網站,在該網站中,它向 Oracle 伺服器產品和伺服器產品附帶的用戶端元件發布修補程式。 這些修補程式是幾個 Microsoft 產品和技術正常運行所必需的。 有關此網站的詳細資訊,請參閱[Oracle 軟體修補程式](../../odbc/microsoft/oracle-software-patches.md)。  
  
> [!CAUTION]  
>  通過 MDAC/Windows DAC 安裝 Oracle 軟體可能會覆蓋 MDAC 的當前版本。 如果使用 ODBC 元件出現問題,請重新安裝 MDAC。
