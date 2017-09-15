---
title: "32 位元驅動程式搭配使用 16 位元和 32 位元應用程式 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC drivers [ODBC], 16-bit applications
- ODBC drivers [ODBC], 32-bit applications
- 32-bit applications with 32-bit drivers [ODBC]
- 16-bit applications with 32-bit drivers [ODBC]
ms.assetid: fc65c988-b31f-4cc9-851f-30d2119604fd
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 802b09dd83ce3671edbff33ff2be447c6279621f
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="using-16-bit-and-32-bit-applications-with-32-bit-drivers"></a>16 位元和 32 位元應用程式使用 32 位元驅動程式
> [!IMPORTANT]  
>  16 位元應用程式支援將未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 而是開發 32 位元或 64 位元應用程式。  
  
 ODBC 資料存取元件，您可以使用 16 位元和 32 位元與 32 位元驅動程式的應用程式。 Microsoft® Windows® 95/98 及 Microsoft Windows/Windows 2000 作業系統支援的應用程式與驅動程式的下列組合：  
  
-   16 位元與 32 位元驅動程式的應用程式  
  
-   32 位元與 32 位元驅動程式的應用程式  
  
 不支援 32 位元應用程式使用的 16 位元驅動程式。  
  
> [!NOTE]  
>  從 ODBC 3.0 版的版本開始，Windows NT 4.0 支援。  
  
 ODBC 包括 ODBC 所需的元件支援上述的設定 」 thunk"動態連結程式庫 (Dll)，將 16 位元位址轉換為 32 位元位址，反之亦然。 安裝程式會判斷您使用並安裝 ODBC 元件，該系統所需的作業系統。 您也可以選擇安裝所有系統所使用的 ODBC 元件。  
  
 在大部分情況下，移轉應用程式或驅動程式從 16 位元為 32 位元包含五種類型的變更：  
  
-   變更訊息處理的程式碼  
  
-   因為有 32 位元整數和控制代碼會變更  
  
-   呼叫 Windows 應用程式開發介面 (Api) 中的變更  
  
-   讓驅動程式的安全執行緒的變更  
  
-   對 ODBC 元件  
  
 從應用程式或驅動程式程式設計的觀點而言，16 位元和 32 位元 ODBC 元件之間的主要差異是它們有不同的檔案名稱。 系統的觀點而言，每個應用程式或驅動程式連接的架構不相同和用來管理資料來源的工具不同。  
  
 此章節包含下列主題。  
  
-   [16 位元應用程式使用 32 位元驅動程式](../../odbc/microsoft/using-16-bit-applications-with-32-bit-drivers.md)  
  
-   [32 位元應用程式使用 32 位元驅動程式](../../odbc/microsoft/using-32-bit-applications-with-32-bit-drivers.md)
