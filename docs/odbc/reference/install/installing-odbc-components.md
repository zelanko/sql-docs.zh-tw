---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b5f033ac12569c7de61af071930d6c8d58d8b611
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63198222"
---
# <a name="installing-odbc-components"></a>安裝 ODBC 元件
> [!NOTE]  
>  從 Windows XP 和 Windows Server 2003 開始，ODBC 會包含在 Windows 作業系統。 您只明確應該安裝在舊版 Windows 上的 ODBC。  
  
 本章節描述如何安裝及移除 ODBC 元件。 驅動程式開發人員一律會安裝 ODBC 元件 （其驅動程式），因為它們需要閱讀本節。 應用程式開發人員需要在閱讀本節，只有當他們將提供與應用程式的 ODBC 元件。 ODBC 元件包括驅動程式管理員、 驅動程式、 翻譯工具、 安裝程式 DLL、 資料指標程式庫，以及任何相關的檔案。 基於本章節的目的，ODBC 應用程式較不是 ODBC 元件。  
  
> [!NOTE]  
>  本節是 Microsoft Windows 平台專用的。 其他平台上安裝 ODBC 元件的方式是特定平台。  
  
 ODBC 元件安裝和移除以元件的元件為基礎，而不以檔案的方式為基礎。 比方說，如果轉譯器所組成，轉譯器本身與資料檔案的數目，這些檔案會安裝和移除某個群組;他們必須安裝及移除檔案的方式為基礎。 這是確保僅有的完整元件存在於系統。  
  
 為了安裝和移除元件，以下被定義為 ODBC 元件：  
  
-   **核心元件。** 驅動程式管理員、 資料指標程式庫、 安裝程式 DLL，和任何其他相關檔案組成的核心元件和必須安裝和移除群組。  
  
-   **驅動程式。** 每個驅動程式是個別的元件。  
  
-   **轉譯器。** 每 translator 是個別的元件。  
  
 Unicode ODBC 3.5 和更新版本的支援，必須提供一些考量搭配 ODBC 使用 OLE DB 元件。 在 ODBC 3.0 中的特定 Unicode 規格寫入 1.1 版的 OLE DB Provider for ODBC。 在 ODBC 3.5 中，變更這些規格，因為它需要 1.5 版或更新版本的提供者時使用 ODBC 3.5 和更新版本。 此章節包含下列主題。  
  
-   [安裝元件](../../../odbc/reference/install/installation-components.md)  
  
-   [使用計數](../../../odbc/reference/install/usage-counting.md)
