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
ms.openlocfilehash: 7dfc63aaa6f162d382d6d8b3c627ff078c76825c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68079059"
---
# <a name="prompting-the-user-for-connection-information"></a>提示使用者輸入連線資訊
如果應用程式使用**SQLConnect** ，而且需要提示使用者輸入任何連接資訊，例如使用者名稱和密碼，則必須自行執行。 雖然這可讓應用程式控制其「外觀與風格」，但它可能會強制應用程式包含驅動程式特定的程式碼。 當應用程式需要提示使用者提供驅動程式特定的連接資訊時，就會發生這種情況。 這對於一般應用程式而言是不可能的情況，而這是設計用來處理任何和所有驅動程式，包括撰寫應用程式時不存在的驅動程式。  
  
 **SQLDriverConnect**可以提示使用者輸入連接資訊。 例如，先前提到的自訂程式可能會將下列連接字串傳遞至**SQLDriverConnect**：  
  
```  
DSN=XYZ Corp;  
```  
  
 然後，驅動程式可能會顯示一個對話方塊，提示您輸入使用者識別碼和密碼，如下圖所示。  
  
 ![提示輸入使用者 ID 與密碼的對話方塊](../../../odbc/reference/develop-app/media/pr18.gif "pr18")  
  
 驅動程式可能會提示連接資訊，特別適用于一般和垂直應用程式。 這些應用程式不應該包含驅動程式特定的資訊，而且驅動程式會提示您提供所需的資訊，以防止應用程式的資訊。 先前的兩個範例會顯示這種情況。 當應用程式只將資料來源名稱傳遞至驅動程式時，應用程式不會包含任何驅動程式特定的資訊，因此不會系結至特定驅動程式。 當應用程式將完整的連接字串傳遞至驅動程式時，它會系結至可以解讀該字串的驅動程式。  
  
 一般應用程式可能會進一步執行此步驟，而不是指定資料來源。 當**SQLDriverConnect**收到空的連接字串時，驅動程式管理員會顯示下列對話方塊。  
  
 ![[選取資料來源] 對話方塊](../../../odbc/reference/develop-app/media/ch06a.gif "CH06A")  
  
 在使用者選取資料來源之後，驅動程式管理員會建立指定該資料來源的連接字串，並將它傳遞給驅動程式。 然後，驅動程式會提示使用者提供它所需的任何其他資訊。  
  
 驅動程式提示使用者由*DriverCompletion*旗標控制的條件;有一些選項可一律提示，如有必要則提示，或永遠不提示。 如需此旗標的完整說明，請參閱[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)函數描述。
