---
description: 硬體和軟體需求 (ODBC)
title: " (ODBC) 的硬體和軟體需求 |Microsoft Docs"
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
ms.openlocfilehash: a0f88c8877161122c11fb65bcdb62fd4e7b684c3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88412484"
---
# <a name="hardware-and-software-requirements-odbc"></a>硬體和軟體需求 (ODBC)
本主題列出使用 ODBC 桌面資料庫驅動程式的需求。  
  
## <a name="hardware-requirements"></a>硬體需求  
 若要使用 ODBC Desktop 資料庫驅動程式，您必須具備：  
  
-   IBM 相容的個人電腦。  
  
-   具有 6 MB 可用磁碟空間的硬碟。  
  
-   至少 16 MB 的隨機存取記憶體 (RAM) 。  
  
## <a name="software-requirements"></a>軟體需求  
 若要使用 ODBC 驅動程式來存取資料，您必須具備：  
  
-   ODBC 驅動程式。  
  
-   32位 ODBC 驅動程式管理員3.51 版或更新版本 ( # A0) 。  
  
-   Microsoft Windows 95 或更新版本，或 Windows NT 4.0 或 Windows 2000。  
  
-   使用 Microsoft ODBC 驅動程式的應用程式至少有 20 KB 的堆疊大小。  
  
 使用 Microsoft Windows NT 4.0 或 Windows 2000 時，32位驅動程式是安全線程，但只能透過使用控制驅動程式存取的全域信號。 在 Windows NT 下，驅動程式的並行使用非常有限。 所有使用 Microsoft Jet 引擎的應用程式，對 Jet ISAM 層的所有存取都是單一執行緒。  
  
 在 Windows 上的 Windows 上執行多個16位應用程式 (WOW) 在 Microsoft Windows NT 4.0 上，應用程式必須在不同的記憶體空間中執行。  (無法使用相同的記憶體空間，因為 ODBC 在相同的進程中不支援多個環境。 ) 若要在不同的記憶體空間中執行應用程式，請在 [程式管理員] 中選取應用程式的圖示，開啟 [檔案 **] 功能表，** 然後按一下 [ **屬性**]，再按一下 [ **在不同的記憶體空間中執行**]。  
  
 不支援 Windows 95 上的16位應用程式使用這些驅動程式。  
  
## <a name="driver-specific-hardware-and-software-requirements"></a>驅動程式特定的硬體和軟體需求  
  
-   MicrosoftAccess 和 dBASEdrivers 可能需要 Autoexec.bat 或 Config.sys 檔案中的變更。
