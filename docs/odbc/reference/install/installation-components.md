---
title: 安裝元件 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- installing ODBC components [ODBC], setup program
- ODBC [ODBC], component installation
ms.assetid: 9de15ca0-fe6a-4634-8709-a928d3c9cc73
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a883377a17aa9e0c3426b4805263616375ea6215
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/11/2018
ms.locfileid: "53208777"
---
# <a name="installation-components"></a>安裝元件
> [!NOTE]  
>  從 Windows XP 和 Windows Server 2003 開始，ODBC 會包含在 Windows 作業系統。 您只明確應該安裝在舊版 Windows 上的 ODBC。  
  
 使用者執行安裝程式時，會啟動安裝程序。 安裝程式可搭配*安裝程式 DLL*並*驅動程式安裝 DLL*每個驅動程式。 安裝程式並安裝程式 DLL 使用中的引數**SQLInstallDriverEx**並**SQLInstallTranslatorEx**函式來判斷哪些檔案来複製或刪除每個元件。 下圖顯示這些安裝的元件之間的關聯性。  
  
 ![安裝元件之間的關聯性](../../../odbc/reference/install/media/pr29.gif "pr29")  
  
> [!IMPORTANT]
>  ODBC 2 中所使用 Odbc.inf 檔案。*x*來描述每個 ODBC 所需的檔案元件不使用在 ODBC 3 *.x*。 ODBC 3 隨附的驅動程式 *.x*元件不需要建立 Odbc.inf 檔案。 移除**SQLInstallDriver**並**SQLInstallODBC**，並取代**SQLInstallTranslator**，轉譯 Odbc.inf 不必要。 現在提供使用 Driver 關鍵字 Odbc.inf 章節中的驅動程式資訊*lpszDriver*中的引數**SQLInstallDriverEx**。 轉譯器資訊，用來在 [ODBC 轉譯程式] 和轉譯程式規格 Odbc.inf 區段現在提供*lpszTranslator*引數**SQLInstallTranslatorEx**。 這些變更可讓 ODBC 安裝程式，能夠更容易移植到不同的平台。  
  
 如需有關這些元件的詳細資訊，請參閱本節結尾處的下列主題。  
  
-   [安裝程式](../../../odbc/reference/install/setup-program.md)  
  
-   [安裝程式 DLL](../../../odbc/reference/install/installer-dll.md)  
  
-   [驅動程式安裝程式 DLL](../../../odbc/reference/install/driver-setup-dll.md)
