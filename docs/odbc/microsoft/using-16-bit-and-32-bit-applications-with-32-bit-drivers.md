---
title: 使用 16 位元和 32 位元應用程式,使用 32 位元驅動程式 |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7ce996a7c4816d4d14491e226f891904b6cf8c02
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307609"
---
# <a name="using-16-bit-and-32-bit-applications-with-32-bit-drivers"></a>搭配使用 16 位元和 32 位元應用程式與 32 位元驅動程式
> [!IMPORTANT]  
>  16 位元應用程式支援將在將來版本的 Windows 中刪除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 開發 32 位元或 64 位元應用程式。  
  
 使用 ODBC 資料存取元件,您可以使用具有 32 位元驅動程式的 16 位元和 32 位元應用程式。 微軟® Windows ® 95/98 和微軟 Windows NT®/Windows 2000 作業系統支援以下應用程式和驅動程式的組合:  
  
-   具有 32 位元驅動程式的 16 位元應用程式  
  
-   32 位元應用程式,具有 32 位元驅動程式  
  
 不支援使用具有 16 位驅動程式的 32 位元應用程式。  
  
> [!NOTE]  
>  從 ODBC 版本 3.0 的發表開始,Windows NT 4.0 一直支援。  
  
 ODBC 包括支援上述配置所需的 ODBC 元件,透過「瀏覽」動態連結庫 (DLL) 將 16 位元位址轉換為 32 位元位址,反之亦然。 安裝程式確定您正在使用哪個作業系統並安裝該系統所需的 ODBC 元件。 您還可以選擇安裝所有系統使用的 ODBC 元件。  
  
 在大多數情況下,將應用程式或驅動程式從 16 位元移植到 32 位元涉及五種類型的更改:  
  
-   對訊息處理代碼的變更  
  
-   更改,因為整數和句柄為 32 位元  
  
-   對 Windows 應用程式設計介面 (API) 的呼叫中的變更  
  
-   變更以使驅動程式線程安全  
  
-   對 ODBC 元件的變更  
  
 從應用程式或驅動程式編程的角度來看,16 位元和 32 位 ODBC 元件之間的主要區別是它們具有不同的檔名。 從系統的角度來看,每個應用程式或驅動程式連接的體系結構是不同的,用於管理數據源的工具也不同。  
  
 此章節包含下列主題。  
  
-   [搭配使用 16 位元應用程式與 32 位元驅動程式](../../odbc/microsoft/using-16-bit-applications-with-32-bit-drivers.md)  
  
-   [搭配使用 32 位元應用程式與 32 位元驅動程式](../../odbc/microsoft/using-32-bit-applications-with-32-bit-drivers.md)
