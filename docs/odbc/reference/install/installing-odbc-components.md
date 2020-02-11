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
ms.openlocfilehash: bf2ef856d8970bf60b3f1f329c57a2379eb528dc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68094018"
---
# <a name="installing-odbc-components"></a>安裝 ODBC 元件
> [!NOTE]  
>  從 Windows XP 和 Windows Server 2003 開始，ODBC 包含在 Windows 作業系統中。 您只應該在舊版 Windows 上明確安裝 ODBC。  
  
 本節說明如何安裝和移除 ODBC 元件。 因為驅動程式開發人員一律會安裝 ODBC 元件（其驅動程式），所以必須閱讀本節。 只有當應用程式開發人員將 ODBC 元件與應用程式一起傳送時，才需要閱讀本節。 ODBC 元件包括驅動程式管理員、驅動程式、轉譯器、安裝程式 DLL、資料指標程式庫，以及任何相關檔案。 基於本節的目的，ODBC 應用程式不會被視為 ODBC 元件。  
  
> [!NOTE]  
>  本章節專屬於 Microsoft Windows 平臺。 ODBC 元件在其他平臺上的安裝方式是平臺特定的。  
  
 ODBC 元件會依元件逐一安裝和移除，而不是逐檔案。 例如，如果翻譯工具組含翻譯工具本身和數個資料檔案，則會以群組的形式安裝和移除這些檔案;不得以逐檔案方式安裝和移除它們。 這麼做的原因是要確定系統上只有完整的元件存在。  
  
 為了安裝和移除元件，下列內容定義為 ODBC 元件：  
  
-   **核心元件。** 驅動程式管理員、資料指標程式庫、安裝程式 DLL 和任何其他相關檔案都構成核心元件，而且必須以群組的形式安裝和移除。  
  
-   **設備.** 每個驅動程式都是個別的元件。  
  
-   **者.** 每個翻譯工具都是個別的元件。  
  
 在 ODBC 3.5 和更新版本中支援 Unicode，必須提供一些考慮，才能搭配使用 OLE DB 元件與 ODBC。 ODBC 3.0 中的特定 Unicode 規格會將1.1 版的 ODBC OLE DB 提供者寫入。 因為這些規格在 ODBC 3.5 中有所變更，所以在使用 ODBC 3.5 和更新版本時，必須有提供者版本1.5 或更新版本。 此章節包含下列主題。  
  
-   [安裝元件](../../../odbc/reference/install/installation-components.md)  
  
-   [使用計數](../../../odbc/reference/install/usage-counting.md)
