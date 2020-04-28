---
title: 硬體和軟體需求（ODBC） |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81295238"
---
# <a name="hardware-and-software-requirements-odbc"></a>硬體和軟體需求 (ODBC)
本主題列出使用 ODBC 桌面資料庫驅動程式的需求。  
  
## <a name="hardware-requirements"></a>硬體需求  
 若要使用 ODBC 桌面資料庫驅動程式，您必須具備：  
  
-   與 IBM 相容的個人電腦。  
  
-   具有 6 MB 可用磁碟空間的硬碟。  
  
-   至少 16 MB 的隨機存取記憶體（RAM）。  
  
## <a name="software-requirements"></a>軟體需求  
 若要使用 ODBC 驅動程式來存取資料，您必須具備：  
  
-   ODBC 驅動程式。  
  
-   32位的 ODBC 驅動程式管理員，3.51 版或更新版本（Odbc32.lib .dll）。  
  
-   Microsoft Windows 95 或更新版本，或 Windows NT 4.0 或 Windows 2000。  
  
-   使用 Microsoft ODBC 驅動程式之應用程式的堆疊大小至少為 20 KB。  
  
 使用 Microsoft Windows NT 4.0 或 Windows 2000 時，32位驅動程式是安全線程，但只能透過使用控制驅動程式存取的全域信號。 在 Windows NT 底下，驅動程式的並行使用非常有限。 對於所有使用 Microsoft Jet 引擎的應用程式，Jet ISAM 層的所有存取都是單一執行緒。  
  
 在 Microsoft Windows NT 4.0 上于 windows on windows （WOW）上執行多個16位應用程式時，應用程式必須在不同的記憶體空間中執行。 （因為 ODBC 在同一個進程中不支援多個環境，所以無法使用相同的記憶體空間）。若要在不同的記憶體空間中執行應用程式，請在 [程式管理員] 中選取應用程式的圖示，開啟 [檔案 **] 功能表，** 按一下 [內容]，**然後按一下 [****在個別的記憶體空間中執行**]。  
  
 Windows 95 上的16位應用程式不支援使用這些驅動程式。  
  
## <a name="driver-specific-hardware-and-software-requirements"></a>驅動程式特定的硬體和軟體需求  
  
-   MicrosoftAccess 和 dBASEdrivers 可能需要在 Autoexec 或 Config.xml 檔案中進行變更。
