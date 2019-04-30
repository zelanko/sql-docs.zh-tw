---
title: 使用 16 位元和 32 位元應用程式與 32 位元驅動程式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC drivers [ODBC], 16-bit applications
- ODBC drivers [ODBC], 32-bit applications
- 32-bit applications with 32-bit drivers [ODBC]
- 16-bit applications with 32-bit drivers [ODBC]
ms.assetid: fc65c988-b31f-4cc9-851f-30d2119604fd
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8540983b84d4d39fe5a02b92a1e3a3606350d36d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63209992"
---
# <a name="using-16-bit-and-32-bit-applications-with-32-bit-drivers"></a>搭配使用 16 位元和 32 位元應用程式與 32 位元驅動程式
> [!IMPORTANT]  
>  Windows 的未來版本將移除 16 位元應用程式的支援。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 而是開發 32 位元或 64 位元的應用程式。  
  
 使用 ODBC 資料存取元件中，您可以使用 32 位元驅動程式的 16 位元和 32 位元應用程式。 Microsoft® Windows® 95/98 及 Microsoft Windows/Windows 2000 作業系統支援的應用程式與驅動程式的下列組合：  
  
-   32 位元驅動程式的 16 位元應用程式  
  
-   32 位元驅動程式的 32 位元應用程式  
  
 不支援 32 位元應用程式使用的 16 位元驅動程式。  
  
> [!NOTE]  
>  從 ODBC 3.0 版的版本開始，Windows NT 4.0 支援。  
  
 ODBC 包含 ODBC 所需的元件可支援上述的組態"thunk 「 動態連結程式庫 (Dll)，將 16 位元位址轉換為 32 位元位址，反之亦然。 安裝程式會判斷您正在使用並已安裝 ODBC 元件，該系統所需的作業系統。 您也可以選擇安裝所有的系統所使用的 ODBC 元件。  
  
 在大部分情況下，移植應用程式或驅動程式從 16 位元為 32 位元包含五種類型的變更：  
  
-   變更訊息處理的程式碼  
  
-   變更，因為整數和控制代碼是 32 位元  
  
-   在 Windows 應用程式發展介面 (Api) 的呼叫中的變更  
  
-   若要使驅動程式的安全執行緒的變更  
  
-   對 ODBC 元件  
  
 從應用程式或驅動程式的程式設計觀點，16 位元和 32 位元 ODBC 元件的主要差異是它們有不同的檔案名稱。 從系統觀點來看，每個應用程式或驅動程式連線的架構不同，工具可用來管理資料來源之間的差異。  
  
 此章節包含下列主題。  
  
-   [搭配使用 16 位元應用程式與 32 位元驅動程式](../../odbc/microsoft/using-16-bit-applications-with-32-bit-drivers.md)  
  
-   [搭配使用 32 位元應用程式與 32 位元驅動程式](../../odbc/microsoft/using-32-bit-applications-with-32-bit-drivers.md)
