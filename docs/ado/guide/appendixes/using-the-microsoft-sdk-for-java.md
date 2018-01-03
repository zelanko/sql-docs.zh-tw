---
title: "使用 Microsoft SDK for Java |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 02/15/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Java (Microsoft SDK for)
- Microsoft SDK for Java [ADO]
ms.assetid: 2d7cb5b5-8307-49dd-b07e-c07069bb1626
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9374f45cad38152d2b394ab7905943106c231702
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="using-the-microsoft-sdk-for-java"></a>使用 Microsoft SDK for Java

> [!IMPORTANT]
> Microsoft 在 2004 年 1 月停止支援的 Visual J + +。

Microsoft SDK for Java 是 Microsoft Internet Explorer 環境的開發人員套件。 工具、 資訊和範例可協助您開發使用 Java 程式和 JDK 1.1 和 Microsoft Win32 虛擬機器 (Microsoft VM) 為基礎的小程式。 Microsoft SDK for Java 未繫結至 Microsoft Visual J + +。 若要下載這個 SDK，請按一下這裡。  
  
 Jactivex.exe 公用程式會從類型程式庫產生類別，但只在命令列叫用。 這項功能未與 Visual J + + 開發環境整合。 不同於 Java 類型程式庫精靈所產生類別，您可以逐步執行 SDK 所建立的類別包裝函式。 這是適用於偵錯您的程式碼如何使用 ADO 包裝函式類別。  
  
 這項機制會讀取 ADO 型別程式庫，並產生您可以具現化應用程式中的類別。 在下列位置中產生這些類別： \\< windows 目錄\>\Java\trustlib\msado15。  
  
 建立 ADO 應用程式在 Java 中使用 Microsoft SDK for Java 是基本上類似，觀點的程式碼中，使用 Java 類型程式庫精靈。 範例程式碼，請參閱[ADO Java 類別包裝函式](../../../ado/guide/appendixes/ado-java-class-wrappers.md)。 唯一的差別在於中如何產生包裝函式類別在一開始，如下列步驟所示。  
  
### <a name="to-create-an-ado-project-with-the-microsoft-sdk-for-java"></a>建立 ADO 專案使用 Microsoft SDK for Java  
  
1.  在命令提示字元執行下列命令。 您必須設定路徑以包括 Microsoft SDK for Java Bin 目錄，或從該位置執行命令。 通常，Microsoft SDK for Java 會安裝在與 Visual Studio 相同的位置。 這是單一命令陳述式。  
  
    ```  
    \<path to DevStudio>\<path to Java SDK>\bin\JactiveX.exe /javatlb "C:\program files\common files\system\ado\msado15.dll"  
    ```  
  
2.  執行下列命令來編譯所產生的類別。 /G:t 參數會將偵錯符號的產生，以便您可以追蹤到。Java 符號。 請移除它的發行組建。  
  
    ```  
    jvc /g:t c:\<windows>\Java\trustlib\msado15\*.Java  
    ```  
  
3.  若要使用這些檔案，開啟您的專案中 Visual J + +。 從**專案**功能表上，選擇**加入至專案**。 選取**檔案**，並加入所有的。JAVA trustlib\msado15 目錄至您的專案中產生的檔案。  
  
## <a name="see-also"></a>請參閱  
 [ADO Java 類別包裝函式](../../../ado/guide/appendixes/ado-java-class-wrappers.md)   
