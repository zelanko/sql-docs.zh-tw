---
description: 使用 Microsoft SDK for Java
title: 使用 Microsoft SDK for JAVA |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: e6119433c1a5c52e07035d97878155123d787e26
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88453970"
---
# <a name="using-the-microsoft-sdk-for-java"></a>使用 Microsoft SDK for Java

> [!IMPORTANT]
> Microsoft 已停止支援2004年1月的 Visual c + +。

Microsoft SDK for JAVA 是 Microsoft Internet Explorer 環境的開發人員套件。 提供的工具、資訊和範例可協助您根據 JDK 1.1 和 Microsoft Win32 虛擬機器 (Microsoft VM) 開發 JAVA 程式和 applet。 Microsoft SDK for JAVA 未與 Microsoft Visual c + + 系結。 若要下載此 SDK，請按一下這裡。  
  
 Jactivex.exe 公用程式會從類型程式庫產生類別，但是只能在命令列上叫用。 這項功能未與 Visual c + + 開發環境整合。 不同于 JAVA 類型程式庫 Wizard 所產生的類別，您可以逐步執行 SDK 所建立的類別包裝函式。 這適用于偵錯工具代碼使用 ADO 包裝函式類別的方式。  
  
 這種機制會讀取 ADO 類型程式庫，並產生您可以在應用程式內具現化的類別。 它會在下列位置產生這些類別： \\<windows 目錄 \> \JAVA\trustlib\msado15。  
  
 使用 Microsoft SDK for JAVA 以 JAVA 建立 ADO 應用程式基本上是完全相同的，從原始程式碼的觀點來看，使用 JAVA 類型程式庫 Wizard。 如需範例程式碼，請參閱 [ADO JAVA 類別包裝](../../../ado/guide/appendixes/ado-java-class-wrappers.md)函式。 唯一的差異在於您如何在第一個位置產生包裝函式類別，如下列步驟所示。  
  
### <a name="to-create-an-ado-project-with-the-microsoft-sdk-for-java"></a>使用 Microsoft SDK for JAVA 建立 ADO 專案  
  
1.  在命令提示字元中執行下列命令。 您必須將路徑設定為包含 Microsoft SDK for JAVA Bin 目錄，或從該位置執行命令。 一般而言，適用于 JAVA 的 Microsoft SDK 會安裝在與 Visual Studio 相同的位置。 這是單一命令語句。  
  
    ```java
    \<path to DevStudio>\<path to Java SDK>\bin\JactiveX.exe /javatlb "C:\program files\common files\system\ado\msado15.dll"  
    ```  
  
2.  執行下列命令來編譯產生的類別。 /G： t 參數會開啟 debug 符號的產生，讓您可以追蹤至。JAVA 符號。 移除發行組建的。  
  
    ```java
    jvc /g:t c:\<windows>\Java\trustlib\msado15\*.Java  
    ```  
  
3.  若要使用這些檔案，請在 Visual j + + 中開啟您的專案。 從 [ **專案** ] 功能表中，選擇 [ **加入至專案**]。 選取 **[** 檔案]，然後加入所有。在 trustlib\msado15 目錄中為您的專案產生的 JAVA 檔案。  
  
## <a name="see-also"></a>另請參閱  
 [ADO Java 類別包裝函式](../../../ado/guide/appendixes/ado-java-class-wrappers.md)   
