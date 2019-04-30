---
title: 使用 Microsoft SDK for Java |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Java (Microsoft SDK for)
- Microsoft SDK for Java [ADO]
ms.assetid: 2d7cb5b5-8307-49dd-b07e-c07069bb1626
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ab4aaed1cfd661d38476c81f8bdc3dcab3aa0f88
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63199742"
---
# <a name="using-the-microsoft-sdk-for-java"></a>使用 Microsoft SDK for Java

> [!IMPORTANT]
> Microsoft 在 2004 年 1 月停止支援的 Visual J + +。

Microsoft SDK for Java 是 Microsoft Internet Explorer 環境的開發人員套件。 工具、 資訊和範例可協助您開發的 Java 程式及 JDK 1.1 和 Microsoft Win32 虛擬機器 (Microsoft VM) 為基礎的小程式。 Microsoft SDK for Java 未繫結至 Microsoft Visual J + +。 若要下載此 SDK，請按一下這裡。  
  
 Jactivex.exe 公用程式會從類型程式庫產生類別，但只能在命令列上叫用。 這項功能並未整合到 Visual J + + 開發環境。 不同於 Java 型別程式庫精靈所產生類別，您可以逐步執行由 SDK 所建立的類別包裝函式。 這是適用於偵錯您的程式碼如何使用 ADO 包裝函式類別。  
  
 這項機制會讀取 ADO 型別程式庫，並產生您可以具現化您的應用程式內的類別。 在下列位置產生這些類別： \\< windows 目錄\>\Java\trustlib\msado15。  
  
 在 Java 中使用 Microsoft SDK for Java 建立 ADO 應用程式是基本上類似，從來源程式碼的觀點來看使用 Java 型別程式庫精靈。 範例程式碼，請參閱[ADO Java 類別包裝函式](../../../ado/guide/appendixes/ado-java-class-wrappers.md)。 您如何一開始，如下列步驟所示產生包裝函式類別位於唯一的真正差異。  
  
### <a name="to-create-an-ado-project-with-the-microsoft-sdk-for-java"></a>若要使用 Microsoft SDK for Java 建立 ADO 專案  
  
1.  在命令提示字元執行下列命令。 您必須設定要包含 Microsoft SDK for Java 的 Bin 目錄的路徑，或從該位置執行命令。 一般來說，Microsoft SDK for Java 被安裝在與 Visual Studio 相同的位置。 這是單一命令陳述式。  
  
    ```java
    \<path to DevStudio>\<path to Java SDK>\bin\JactiveX.exe /javatlb "C:\program files\common files\system\ado\msado15.dll"  
    ```  
  
2.  執行下列命令來編譯產生的類別。 /G:t 切換開啟偵錯符號的產生，因此您可以追蹤程式。Java 的符號。 表示發行組建中移除它。  
  
    ```java
    jvc /g:t c:\<windows>\Java\trustlib\msado15\*.Java  
    ```  
  
3.  若要使用這些檔案，開啟您的專案中 Visual J + +。 從**專案**功能表上，選擇**加入至專案**。 選取 **檔案**，並將所有加。產生 trustlib\msado15 目錄至您的專案中的 JAVA 檔案。  
  
## <a name="see-also"></a>另請參閱  
 [ADO Java 類別包裝函式](../../../ado/guide/appendixes/ado-java-class-wrappers.md)   
