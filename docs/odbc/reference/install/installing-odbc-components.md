---
description: 安裝 ODBC 元件
title: 安裝 ODBC 元件 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- installing ODBC components [ODBC]
- installing ODBC components [ODBC], about installing
- ODBC [ODBC], component installation
ms.assetid: b7e48e9c-8912-4003-b4ef-30aa44de06a7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0250cc51b76cbda9c1091ebe1d696c2e569c037f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499744"
---
# <a name="installing-odbc-components"></a>安裝 ODBC 元件
> [!NOTE]  
>  從 Windows XP 和 Windows Server 2003 開始，ODBC 會包含在 Windows 作業系統中。 您應該只在舊版的 Windows 上明確地安裝 ODBC。  
  
 本節說明如何安裝和移除 ODBC 元件。 因為驅動程式開發人員一律會 (其驅動程式) 安裝 ODBC 元件，所以需要閱讀本節。 只有當應用程式開發人員會將 ODBC 元件與應用程式一起提供時，才需要閱讀本節。 ODBC 元件包括驅動程式管理員、驅動程式、轉譯程式、安裝程式 DLL、資料指標程式庫，以及任何相關的檔案。 基於本節的目的，ODBC 應用程式不會被視為 ODBC 元件。  
  
> [!NOTE]  
>  本節專屬於 Microsoft Windows 平臺。 在其他平臺上安裝 ODBC 元件的方式是平臺特定的。  
  
 ODBC 元件會依元件個別安裝和移除，而不是逐檔案的方式。 例如，如果翻譯工具是由翻譯工具本身和數個資料檔案所組成，則這些檔案會以群組的形式安裝和移除;它們不得以檔案逐一安裝和移除。 這是為了確保只有完整的元件存在於系統上。  
  
 基於安裝和移除元件的目的，下列定義為 ODBC 元件：  
  
-   **核心元件。** 驅動程式管理員、資料指標程式庫、安裝程式 DLL 和任何其他相關檔案都構成核心元件，而且必須以群組的形式加以安裝和移除。  
  
-   **司機。** 每個驅動程式都是個別的元件。  
  
-   **翻譯。** 每個翻譯工具都是個別的元件。  
  
 使用 ODBC 3.5 和更新版本中的 Unicode 支援時，必須提供一些考慮，才能搭配 ODBC 使用 OLE DB 元件。 ODBC 的 OLE DB Provider for ODBC 的1.1 版本已寫入 ODBC 3.0 內的特定 Unicode 規格。 因為這些規格在 ODBC 3.5 中有所變更，所以在使用 ODBC 3.5 和更新版本時，必須有 version 1.5 或更新版本的提供者。 此章節包含下列主題。  
  
-   [安裝元件](../../../odbc/reference/install/installation-components.md)  
  
-   [使用計數](../../../odbc/reference/install/usage-counting.md)
