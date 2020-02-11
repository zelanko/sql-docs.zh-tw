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
ms.openlocfilehash: 34d1b6d143f6f40d73e2feeb0b718f3c3b3248fe
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68094127"
---
# <a name="installation-components"></a>安裝元件
> [!NOTE]  
>  從 Windows XP 和 Windows Server 2003 開始，ODBC 包含在 Windows 作業系統中。 您只應該在舊版 Windows 上明確安裝 ODBC。  
  
 當使用者執行安裝程式時，就會啟動安裝程式。 安裝程式會與每個驅動程式的*安裝程式 dll*和驅動程式*安裝 dll*搭配運作。 安裝程式和安裝程式 DLL 都會使用**SQLInstallDriverEx**和**SQLInstallTranslatorEx**函式中的引數，來判斷要針對每個元件複製或刪除的檔案。 下圖顯示這些安裝元件之間的關聯性。  
  
 ![安裝元件間的關聯性](../../../odbc/reference/install/media/pr29.gif "pr29")  
  
> [!IMPORTANT]
>  Odbc 3.x 中不會*使用 odbc 2.x 中用來描述*每個 odbc 元件所需檔案的 odbc. *x。* 送出 ODBC 3.x*元件的*驅動程式不需要建立一個 odbc .inf 檔案。 移除**SQLInstallDriver**和**SQLInstallODBC**，以及取代**SQLInstallTranslator**，就會不必要地轉譯 Odbc .inf。 您現在可以在**SQLInstallDriverEx**的*lpszDriver*引數中，使用在 Odbc 的驅動程式關鍵字區段中提供的驅動程式資訊。 在**SQLInstallTranslatorEx**的*lpszTranslator*引數中，現在已提供用於 Odbc 的 [Odbc Translator] 和翻譯工具規格區段中的翻譯工具資訊。 這些變更可讓 ODBC 安裝程式在不同的平臺上更具可攜性。  
  
 如需這些元件的詳細資訊，請參閱本節結尾的下列主題。  
  
-   [安裝程式](../../../odbc/reference/install/setup-program.md)  
  
-   [安裝程式 DLL](../../../odbc/reference/install/installer-dll.md)  
  
-   [驅動程式安裝程式 DLL](../../../odbc/reference/install/driver-setup-dll.md)
