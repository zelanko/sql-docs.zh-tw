---
title: 提示使用者輸入連接資訊 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 58df84bf96306a2cfbc0567a3d5f6cb13514a06e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62861891"
---
# <a name="prompting-the-user-for-connection-information"></a>提示使用者輸入連線資訊
如果應用程式使用**SQLConnect** ，且必須提示使用者輸入的任何連接資訊，例如使用者名稱和密碼，它必須這樣做本身。 這可讓應用程式來控制其 「 外觀與風格 」，它可能會強制應用程式中包含的驅動程式專屬的程式碼。 會發生這種情況是當應用程式必須提示使用者輸入驅動程式特有的連接資訊。 這代表不可能的情況，是專為所有的驅動程式，包括不存在時的應用程式撰寫的驅動程式所使用的泛型應用程式。  
  
 **SQLDriverConnect**可以提示使用者輸入連接資訊。 例如，先前所述的自訂程式可以將傳遞的下列連接字串**SQLDriverConnect**:  
  
```  
DSN=XYZ Corp;  
```  
  
 然後，驅動程式可能會顯示對話方塊，提示您輸入使用者識別碼和密碼，類似下圖。  
  
 ![提示輸入使用者識別碼和密碼的對話方塊](../../../odbc/reference/develop-app/media/pr18.gif "pr18")  
  
 驅動程式可以提示輸入連接資訊是泛型和垂直應用程式特別有用。 這些應用程式不應包含驅動程式特有的資訊，並具有所需之資訊的驅動程式提示，讓資訊保持登出應用程式。 這是先前的兩個範例所示。 當應用程式傳遞至驅動程式時只有資料來源名稱時，應用程式未包含任何驅動程式專屬資訊，並已因此未繫結至特定的驅動程式。 當應用程式會傳遞至驅動程式的完整連接字串時，它已繫結至驅動程式無法解譯該字串。  
  
 一般的應用程式可能會進一步採取此步驟，並甚至不指定資料來源。 當**SQLDriverConnect**收到空的連接字串，則驅動程式管理員會顯示下列對話方塊。  
  
 ![選取資料來源 對話方塊](../../../odbc/reference/develop-app/media/ch06a.gif "CH06A")  
  
 在使用者選取的資料來源之後，驅動程式管理員會建構連接字串，指定該資料來源，並將它傳遞給驅動程式。 驅動程式可以接著會提示使用者輸入任何必要的額外資訊。  
  
 在其驅動程式會提示使用者的條件會受*DriverCompletion*旗標，也會有一律提示，提示您是否有必要，或永遠不會提示選項。 如需此旗標的完整說明，請參閱[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)函式描述。
