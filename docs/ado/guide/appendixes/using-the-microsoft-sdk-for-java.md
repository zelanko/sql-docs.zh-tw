---
title: 使用適用于 JAVA 的 Microsoft SDK |Microsoft Docs
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
ms.openlocfilehash: b0e6c5f2eb5ad792141e77122ff9e132d97f62ae
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67926461"
---
# <a name="using-the-microsoft-sdk-for-java"></a>使用 Microsoft SDK for Java

> [!IMPORTANT]
> Microsoft 已于2004年1月終止支援 Visual j + +。

Microsoft SDK for JAVA 是 Microsoft Internet Explorer 環境的開發人員套件。 提供工具、資訊和範例，以協助您根據 JDK 1.1 和 Microsoft Win32 虛擬機器（Microsoft VM）開發 JAVA 程式和 applet。 Microsoft SDK for JAVA 並未系結至 Microsoft Visual j + +。 若要下載此 SDK，請按一下這裡。  
  
 Jactivex 公用程式會從類型程式庫產生類別，但只能在命令列上叫用。 這項功能並未與 Visual c + + 開發環境整合。 不同于 JAVA 類型程式庫 Wizard 所產生的類別，您可以逐步執行 SDK 所建立的類別包裝函式。 這適用于偵錯工具代碼使用 ADO 包裝函式類別的方式。  
  
 此機制會讀取 ADO 類型程式庫，並產生您可以在應用程式中具現化的類別。 它會在下列位置產生這些類別： \\<windows 目錄\>\JAVA\trustlib\msado15。  
  
 使用適用于 JAVA 的 Microsoft SDK，在 JAVA 中建立 ADO 應用程式基本上完全相同，從原始程式碼的觀點，到使用 JAVA 類型程式庫 Wizard。 如需範例程式碼，請參閱[ADO JAVA 類別包裝](../../../ado/guide/appendixes/ado-java-class-wrappers.md)函式。 唯一的真正差異在於，您會在第一個位置產生包裝函式類別，如下列步驟所示。  
  
### <a name="to-create-an-ado-project-with-the-microsoft-sdk-for-java"></a>若要使用 Microsoft SDK for JAVA 建立 ADO 專案  
  
1.  在命令提示字元中執行下列命令。 您必須設定路徑以包含 Microsoft SDK for JAVA Bin 目錄，或從該位置執行命令。 一般來說，Microsoft SDK for JAVA 會安裝在與 Visual Studio 相同的位置。 這是單一命令語句。  
  
    ```java
    \<path to DevStudio>\<path to Java SDK>\bin\JactiveX.exe /javatlb "C:\program files\common files\system\ado\msado15.dll"  
    ```  
  
2.  執行下列命令來編譯產生的類別。 /G： t 參數會開啟產生的偵錯工具符號，讓您可以追蹤至。JAVA 符號。 將它移除發行組建。  
  
    ```java
    jvc /g:t c:\<windows>\Java\trustlib\msado15\*.Java  
    ```  
  
3.  若要使用這些檔案，請在 Visual j + + 中開啟您的專案。 從 [**專案**] 功能表中，選擇 [**加入至專案**]。 選取 **[** 檔案]，然後新增所有。在 trustlib\msado15 目錄中為您的專案產生的 JAVA 檔案。  
  
## <a name="see-also"></a>另請參閱  
 [ADO Java 類別包裝函式](../../../ado/guide/appendixes/ado-java-class-wrappers.md)   
