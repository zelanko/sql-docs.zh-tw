---
title: 提示使用者輸入連接資訊 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- connecting to data source [ODBC], SqlConnect
- connecting to driver [ODBC], prompting user for information
- connecting to driver [ODBC], SQLConnect
- connecting to driver [ODBC], SQLDriverConnect
- connecting to data source [ODBC], SqlDriverConnect
- SQLConnect function [ODBC], prompting user for connection information
- connecting to data source [ODBC], prompting user for information
- prompting user for connection information [ODBC]
- SQLDriverConnect function [ODBC], prompting user for connection information
ms.assetid: da98e9b9-a4ac-4a9d-bae6-e9252b1fe1e5
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 54d419e83a4a44273b42559e4b1ba300f021f771
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="prompting-the-user-for-connection-information"></a>提示使用者輸入連接資訊
如果應用程式使用**SQLConnect**且需要提示使用者輸入的任何連接資訊，例如使用者名稱和密碼，就必須這麼做本身。 這可讓應用程式來控制其 「 外觀 」，它可能會強制應用程式中包含的驅動程式專屬的程式碼。 會發生這種情況是當應用程式必須提示使用者輸入驅動程式特有的連接資訊。 這會是不可能的狀況，設計來搭配任何和所有的驅動程式，包括驅動程式不存在時的應用程式撰寫的泛型應用程式。  
  
 **SQLDriverConnect**可以提示使用者輸入連接資訊。 例如，先前所述的自訂程式無法傳遞的下列連接字串**SQLDriverConnect**:  
  
```  
DSN=XYZ Corp;  
```  
  
 驅動程式可能會再顯示對話方塊提示輸入使用者識別碼和密碼下, 圖類似。  
  
 ![提示輸入使用者識別碼和密碼的對話方塊](../../../odbc/reference/develop-app/media/pr18.gif "pr18")  
  
 驅動程式可以提示輸入連接資訊是特別適用於泛型和垂直應用程式。 這些應用程式不能包含驅動程式特有的資訊，而且需要的驅動程式提示字元中所需的資訊會保留該應用程式的資訊。 這是先前兩個範例所示。 應用程式只有資料來源的名稱給驅動程式，應用程式未包含任何驅動程式特定資訊，並已因此未繫結至特定的驅動程式。 當應用程式會傳遞至驅動程式的完整連接字串時，它已連結到該字串無法解譯的驅動程式。  
  
 泛型應用程式可能會進一步採取此步驟，甚至不能指定資料來源。 當**SQLDriverConnect**收到空的連接字串，則驅動程式管理員會顯示下列對話方塊。  
  
 ![選取資料來源對話方塊](../../../odbc/reference/develop-app/media/ch06a.gif "CH06A")  
  
 在使用者選取的資料來源之後，驅動程式管理員建構連接字串，指定該資料來源，並將它傳遞至驅動程式。 驅動程式可以接著會提示使用者輸入任何必要的額外資訊。  
  
 在驅動程式會提示使用者的條件，皆受*DriverCompletion*旗標，也會有一律提示、 出現提示，如果有必要，或永遠不會提示選項。 這個旗標的完整說明，請參閱[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)函式描述。
