---
description: 安裝元件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: aac17b66b52b6d5b167f670302b8e1df14f8907a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499821"
---
# <a name="installation-components"></a>安裝元件
> [!NOTE]  
>  從 Windows XP 和 Windows Server 2003 開始，ODBC 會包含在 Windows 作業系統中。 您應該只在舊版的 Windows 上明確地安裝 ODBC。  
  
 安裝程式會在使用者執行安裝程式時啟動。 安裝程式可搭配 *安裝程式 dll* 和每個驅動程式的 *驅動程式安裝 dll* 一起使用。 安裝程式和安裝程式 DLL 都會使用 **SQLInstallDriverEx** 和 **SQLInstallTranslatorEx** 函式中的引數，來判斷要複製或刪除每個元件的檔案。 下圖顯示這些安裝元件之間的關聯性。  
  
 ![安裝元件間的關聯性](../../../odbc/reference/install/media/pr29.gif "pr29")  
  
> [!IMPORTANT]
>  Odbc 2.x 中所使用的 Odbc .inf 檔案不會 *用來描述* 每 *個 odbc 元件*所需的檔案。 傳送 ODBC 3.x 元件的驅動程式不需要 *建立 odbc .inf* 檔案。 **SQLInstallDriver**和**SQLInstallODBC**的移除以及**SQLInstallTranslator**的取代已轉譯為不需要的 Odbc .inf。 在**SQLInstallDriverEx**的*lpszDriver*引數中，現在提供了使用於 Odbc 之 driver 關鍵字區段的驅動程式資訊。 在**SQLInstallTranslatorEx**的*lpszTranslator*引數中，現在提供了在 odbc 的 [odbc 轉譯器] 和 translator 規格區段中使用的翻譯工具資訊。 這些變更可讓 ODBC 安裝程式更能跨平臺移植。  
  
 如需這些元件的詳細資訊，請參閱本節結尾的下列主題。  
  
-   [安裝程式](../../../odbc/reference/install/setup-program.md)  
  
-   [安裝程式 DLL](../../../odbc/reference/install/installer-dll.md)  
  
-   [驅動程式安裝程式 DLL](../../../odbc/reference/install/driver-setup-dll.md)
