---
title: "硬體和軟體需求 (ODBC) |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- hardware requirements [ODBC], desktop database drivers
- software requirements [ODBC], desktop database drivers
- system requirements [ODBC], desktop database drivers
- requirements [ODBC], desktop database drivers
ms.assetid: 6df2e9cd-de10-4629-97bd-32f2782616c7
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2545fba508ef3862834743ddaa8dd74183123b30
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="hardware-and-software-requirements-odbc"></a>硬體和軟體需求 (ODBC)
本主題列出使用 ODBC 桌面資料庫驅動程式的需求。  
  
## <a name="hardware-requirements"></a>硬體需求  
 若要使用 ODBC 桌面資料庫驅動程式，您必須：  
  
-   在 IBM 相容的個人電腦。  
  
-   具有 6 MB 的可用磁碟空間的硬碟。  
  
-   至少 16 MB 的隨機存取記憶體 (RAM)。  
  
## <a name="software-requirements"></a>軟體需求  
 若要存取與 ODBC 驅動程式的資料，您必須：  
  
-   ODBC 驅動程式。  
  
-   32 位元 ODBC 驅動程式管理員，3.51 版或更新版本 (Odbc32.dll)。  
  
-   Microsoft Windows 95 或更新版本，或 Windows NT 4.0 或 Windows 2000。  
  
-   至少 20 KB 應用程式使用的 Microsoft ODBC 驅動程式的堆疊大小。  
  
 使用 Microsoft Windows NT 4.0 或 Windows 2000 時，32 位元驅動程式是安全執行緒，但只能透過全域信號控制存取驅動程式使用。 同時使用的驅動程式是非常有限 Windows NT 下。 所有存取 Jet ISAM 層將都會使用 Microsoft Jet 引擎的所有應用程式的單一執行緒。  
  
 當 Windows on Windows (WOW) Microsoft Windows NT 4.0 上執行多個 16 位元應用程式，必須在單獨記憶體空間中執行應用程式。 （相同的記憶體空間不能因為 ODBC 不支援多個環境中相同的程序。）若要執行應用程式在不同的記憶體空間中，選取應用程式的圖示 程式管理員 中開啟**檔案**功能表，然後按一下**屬性**，然後按一下 **執行於不同的記憶體空間**。  
  
 不支援這些驅動程式在 Windows 95 上的 16 位元應用程式的使用。  
  
## <a name="driver-specific-hardware-and-software-requirements"></a>驅動程式專用的硬體和軟體需求  
  
-   MicrosoftAccess 和 dBASEdrivers 可能需要的 Autoexec.bat 或 Config.sys 檔案中的變更。

