---
description: 搭配使用 16 位元和 32 位元應用程式與 32 位元驅動程式
title: 搭配使用16位和32位的應用程式與32位驅動程式 |Microsoft Docs
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
ms.openlocfilehash: b3985fa6fa4fd24ad9638e418915542b48abc26f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471373"
---
# <a name="using-16-bit-and-32-bit-applications-with-32-bit-drivers"></a>搭配使用 16 位元和 32 位元應用程式與 32 位元驅動程式
> [!IMPORTANT]  
>  未來的 Windows 版本將會移除16位應用程式支援。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 改為開發32位或64位應用程式。  
  
 使用 ODBC 資料存取元件時，您可以使用具有32位驅動程式的16位和32位應用程式。 Microsoft® Windows®95/98 和 Microsoft Windows NT®/Windows 2000 作業系統支援下列應用程式和驅動程式組合：  
  
-   具有32位驅動程式的16位應用程式  
  
-   具有32位驅動程式的32位應用程式  
  
 不支援搭配使用32位的應用程式與16位驅動程式。  
  
> [!NOTE]  
>  從 ODBC 3.0 版開始，已支援 Windows NT 4.0。  
  
 ODBC 包含透過「Thunking」動態連結程式庫 (Dll 來支援上述設定所需的 ODBC 元件) 將16位位址轉換成32位位址，反之亦然。 安裝程式會決定您使用的作業系統，並安裝該系統所需的 ODBC 元件。 您也可以選擇安裝所有系統所使用的 ODBC 元件。  
  
 在大部分的情況下，將應用程式或驅動程式從16位移植到32位牽涉到五種類型的變更：  
  
-   訊息處理常式代碼的變更  
  
-   因為整數和控制碼為32位，所以變更  
  
-   對 Windows 應用程式開發介面呼叫的變更 (Api)   
  
-   將驅動程式設為安全線程的變更  
  
-   ODBC 元件的變更  
  
 從應用程式或驅動程式設計的觀點來看，16位與32位 ODBC 元件之間的主要差異在於它們具有不同的檔案名。 從系統的觀點來看，每個應用程式或驅動程式連接的架構都不同，而用來管理資料來源的工具則不同。  
  
 此章節包含下列主題。  
  
-   [搭配使用 16 位元應用程式與 32 位元驅動程式](../../odbc/microsoft/using-16-bit-applications-with-32-bit-drivers.md)  
  
-   [搭配使用 32 位元應用程式與 32 位元驅動程式](../../odbc/microsoft/using-32-bit-applications-with-32-bit-drivers.md)
