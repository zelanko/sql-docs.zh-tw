---
title: 使用16位和32位應用程式搭配32位驅動程式 |Microsoft Docs
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
ms.openlocfilehash: 941c821d7622b2364ec1cd417dd9b50302540b95
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68088176"
---
# <a name="using-16-bit-and-32-bit-applications-with-32-bit-drivers"></a>搭配使用 16 位元和 32 位元應用程式與 32 位元驅動程式
> [!IMPORTANT]  
>  在未來的 Windows 版本中，將會移除16位的應用程式支援。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 請改為開發32位或64位的應用程式。  
  
 使用 ODBC 資料存取元件時，您可以使用16位和32位的應用程式搭配32位驅動程式。 Microsoft® Windows®95/98 和 Microsoft Windows NT®/Windows 2000 作業系統支援下列應用程式和驅動程式組合：  
  
-   具有32位驅動程式的16位應用程式  
  
-   具有32位驅動程式的32位應用程式  
  
 不支援搭配使用32位應用程式與16位驅動程式。  
  
> [!NOTE]  
>  從 ODBC 3.0 版開始，已支援 Windows NT 4.0。  
  
 ODBC 包含支援上述設定所需的 ODBC 元件，方法是「Thunking」動態連結程式庫（Dll），將16位位址轉換成32位位址，反之亦然。 安裝程式會決定您使用的作業系統，並安裝該系統所需的 ODBC 元件。 您也可以選擇安裝所有系統使用的 ODBC 元件。  
  
 在大部分的情況下，將應用程式或驅動程式從16位移植到32位會牽涉到五種類型的變更：  
  
-   訊息處理常式代碼的變更  
  
-   因為整數和控制碼為32位，所以變更  
  
-   對 Windows 應用程式開發介面（Api）呼叫的變更  
  
-   讓驅動程式安全線程的變更  
  
-   ODBC 元件的變更  
  
 就應用程式或驅動程式設計的觀點而言，16位和32位 ODBC 元件之間的主要差異在於它們有不同的檔案名。 從系統的觀點來看，每個應用程式或驅動程式連接的架構不同，而用來管理資料來源的工具則有所不同。  
  
 此章節包含下列主題。  
  
-   [搭配使用 16 位元應用程式與 32 位元驅動程式](../../odbc/microsoft/using-16-bit-applications-with-32-bit-drivers.md)  
  
-   [搭配使用 32 位元應用程式與 32 位元驅動程式](../../odbc/microsoft/using-32-bit-applications-with-32-bit-drivers.md)
