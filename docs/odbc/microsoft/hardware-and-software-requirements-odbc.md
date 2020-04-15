---
title: 硬體和軟體要求 (ODBC) |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- hardware requirements [ODBC], desktop database drivers
- software requirements [ODBC], desktop database drivers
- system requirements [ODBC], desktop database drivers
- requirements [ODBC], desktop database drivers
ms.assetid: 6df2e9cd-de10-4629-97bd-32f2782616c7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fe69775e379e9a9d661b4ddf81e577b738fcf34d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81295238"
---
# <a name="hardware-and-software-requirements-odbc"></a>硬體和軟體需求 (ODBC)
本主題列出了使用 ODBC 桌面資料庫驅動程式的要求。  
  
## <a name="hardware-requirements"></a>硬體需求  
 要使用 ODBC 桌面資料庫驅動程式,您必須具有:  
  
-   與 IBM 相容的個人電腦。  
  
-   具有 6 MB 可用磁碟空間的硬碟。  
  
-   至少 16 MB 的隨機存取記憶體 (RAM)。  
  
## <a name="software-requirements"></a>軟體需求  
 要使用 ODBC 驅動程式存取資料,您必須具有:  
  
-   ODBC 驅動程式。  
  
-   32 位元 ODBC 驅動程式管理員,版本 3.51 或更高版本(Odbc32.dll)。  
  
-   微軟視窗 95 或更高版本,或 Windows NT 4.0 或 Windows 2000。  
  
-   使用 Microsoft ODBC 驅動程式的應用程式的堆疊大小至少為 20 KB。  
  
 使用 Microsoft Windows NT 4.0 或 Windows 2000 時,32 位元驅動程式是線程安全的,但只能通過使用控制對驅動程式訪問的全域信號量。 在 Windows NT 下,驅動程式的併發使用非常有限。 對於使用 Microsoft Jet 引擎的所有應用程式,對 Jet ISAM 層的所有訪問都將是單線程的。  
  
 在 Microsoft Windows NT 4.0 上的 Windows 上運行多個 16 位元應用程式時,這些應用程式必須在單獨的記憶體空間中運行。 (不能使用相同的記憶體空間,因為 ODBC 不支援同一進程中的多個環境。要在單獨的記憶體空間中運行應用程式,請在程式管理器中選擇應用程式的圖示,打開 **「檔案**」功能表擊「**屬性**」,然後按一下「**在單獨的記憶體空間中執行**」。  
  
 不支援在 Windows 95 上使用 16 位元應用程式使用這些驅動程式。  
  
## <a name="driver-specific-hardware-and-software-requirements"></a>特定於驅動程式的硬體與軟體需求  
  
-   MicrosoftAccess 和 dBASE 驅動程式可能需要更改 Autoexec.bat 或 Config.sys 檔中。
