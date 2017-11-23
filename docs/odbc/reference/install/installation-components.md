---
title: "安裝元件 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- installing ODBC components [ODBC], setup program
- ODBC [ODBC], component installation
ms.assetid: 9de15ca0-fe6a-4634-8709-a928d3c9cc73
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: e00b3288b224f054939c75201a7ddd44f70c374c
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="installation-components"></a>安裝元件
> [!NOTE]  
>  從 Windows XP 和 Windows Server 2003，ODBC 隨附於 Windows 作業系統。 您只明確應該在舊版 Windows 上安裝 ODBC。  
  
 使用者執行安裝程式時，就會開始安裝程序。 安裝程式可搭配*installer DLL*和*驅動程式安裝 DLL*每個驅動程式。 安裝程式和 DLL，安裝程式使用中的引數**SQLInstallDriverEx**和**SQLInstallTranslatorEx**函式來判斷要複製或刪除每個元件的檔案。 下圖顯示這些安裝元件之間的關聯性。  
  
 ![安裝元件之間的關聯性](../../../odbc/reference/install/media/pr29.gif "pr29")  
  
> [!IMPORTANT]  
>  ODBC 2 中使用 Odbc.inf 檔案。*x*來描述每個 ODBC 所需的檔案元件不是在 ODBC 3*.x*。 驅動程式隨附 ODBC 3*.x*元件不需要建立 Odbc.inf 檔案。 移除**SQLInstallDriver**和**SQLInstallODBC**，並取代的**SQLInstallTranslator**，轉譯 Odbc.inf 非必要。 使用 Driver 關鍵字各 Odbc.inf 的驅動程式的資訊現已提供中*lpszDriver*引數中的**SQLInstallDriverEx**。 用於 [ODBC 轉譯程式] 中的轉譯程式資訊和 Odbc.inf 轉譯器規格區段現在提供在*lpszTranslator*引數的**SQLInstallTranslatorEx**。 這些變更可讓 ODBC 安裝程式能夠更容易移植到不同的平台。  
  
 如需有關這些元件的詳細資訊，請參閱本節結尾處的下列主題。  
  
-   [安裝程式](../../../odbc/reference/install/setup-program.md)  
  
-   [安裝程式 DLL](../../../odbc/reference/install/installer-dll.md)  
  
-   [驅動程式安裝程式 DLL](../../../odbc/reference/install/driver-setup-dll.md)
