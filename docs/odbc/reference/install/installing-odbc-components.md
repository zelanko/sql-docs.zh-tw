---
title: "安裝 ODBC 元件 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- installing ODBC components [ODBC]
- installing ODBC components [ODBC], about installing
- ODBC [ODBC], component installation
ms.assetid: b7e48e9c-8912-4003-b4ef-30aa44de06a7
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 790d398aff2723557f0e944fad87cd03fbc9819c
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="installing-odbc-components"></a>安裝 ODBC 元件
> [!NOTE]  
>  從 Windows XP 和 Windows Server 2003，ODBC 隨附於 Windows 作業系統。 您只明確應該在舊版 Windows 上安裝 ODBC。  
  
 本章節描述如何安裝和移除 ODBC 元件。 驅動程式開發人員一律安裝的 ODBC 元件 （其驅動程式），因為他們需要先閱讀本節。 在閱讀本節，它們將出貨 ODBC 元件和應用程式時，才需要應用程式開發人員。 ODBC 元件包括驅動程式管理員、 驅動程式、 轉譯程式、 安裝程式 DLL、 資料指標程式庫，以及任何相關的檔案。 基於本章節的目的，ODBC 應用程式是不被視為 ODBC 元件。  
  
> [!NOTE]  
>  此區段是 Microsoft Windows 平台專用的。 ODBC 元件安裝在其他平台上的方式是特定平台。  
  
 ODBC 元件安裝和移除以元件的元件為基礎，而不以檔案的檔案為基礎。 例如，如果轉譯器包含轉譯程式本身和資料檔案的數目，這些檔案會安裝和移除某個群組;它們必須安裝及移除檔案的檔案為基礎。 這是確定只有完整的元件都存在於系統上。  
  
 為了安裝和移除元件，以下被定義為 ODBC 元件：  
  
-   **核心元件。** 驅動程式管理員、 資料指標程式庫，安裝程式的 DLL，和任何其他相關檔案組成的核心元件，並且必須安裝和群組中移除。  
  
-   **驅動程式。** 每個驅動程式是個別的元件。  
  
-   **轉譯器。** 每個轉譯器是個別的元件。  
  
 Unicode ODBC 3.5 和更新版本的支援，必須給予某些考量搭配 ODBC 使用 OLE DB 元件。 1.1 版的 OLE DB provider for ODBC 會寫入至特定的 Unicode 規格，在 ODBC 3.0。 在 ODBC 3.5 中，變更這些規格，因為它是需要 1.5 版或更新版本的提供者時使用 ODBC 3.5 和更新版本。 此章節包含下列主題。  
  
-   [安裝元件](../../../odbc/reference/install/installation-components.md)  
  
-   [使用計數](../../../odbc/reference/install/usage-counting.md)
