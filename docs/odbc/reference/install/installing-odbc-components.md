---
title: 安裝 ODBC 元件 :微軟文件
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
ms.openlocfilehash: bbd0a6aeba8073ce14b08b8635396b1f231895fb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298978"
---
# <a name="installing-odbc-components"></a>安裝 ODBC 元件
> [!NOTE]  
>  從 Windows XP 和 Windows 伺服器 2003 開始,ODBC 包含在 Windows 作業系統中。 您只應在早期版本的 Windows 上顯式安裝 ODBC。  
  
 本節介紹如何安裝和刪除 ODBC 元件。 由於驅動程式開發人員始終安裝 ODBC 元件(其驅動程式),因此他們需要閱讀此部分。 應用程式開發人員只有在將 ODBC 元件隨其應用程式一起提供時,才需要閱讀本節。 ODBC 元件包括驅動程式管理器、驅動程式、翻譯人員、安裝程式 DLL、游標庫和任何相關文件。 就本節而言,ODBC 應用程式不被視為 ODBC 元件。  
  
> [!NOTE]  
>  本節特定於 Microsoft Windows 平臺。 如何在其他平臺上安裝ODBC元件是特定於平臺的。  
  
 ODBC 元件是逐個元件安裝和刪除的,而不是逐個檔的。 例如,如果譯員本身和多個數據檔組成,這些檔將作為一個組進行安裝和刪除;不得逐個檔安裝和刪除它們。 這樣做的原因是為了確保系統上僅存在完整的元件。  
  
 為了安裝和拆卸元件,以下定義為 ODBC 元件:  
  
-   **核心元件。** 驅動程式管理員、游標庫、安裝程式 DLL 和任何其他相關文件組成核心元件,必須作為一個組進行安裝和刪除。  
  
-   **司機。** 每個驅動程式都是單獨的元件。  
  
-   **翻譯。** 每個轉換器都是一個單獨的元件。  
  
 在 ODBC 3.5 及更高版本中 Unicode 的支援下,必須考慮將 OLE DB 元件與 ODBC 一起使用。 ODBC 的 OLE DB 提供程式的 1.1 版本寫入了 ODBC 3.0 中的特定 Unicode 規範。 由於這些規範在 ODBC 3.5 中發生了變化,因此在使用 ODBC 3.5 及更高版本時,有必要擁有提供程式的版本 1.5 或更高版本。 此章節包含下列主題。  
  
-   [安裝元件](../../../odbc/reference/install/installation-components.md)  
  
-   [使用計數](../../../odbc/reference/install/usage-counting.md)
