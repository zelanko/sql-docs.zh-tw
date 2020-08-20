---
description: 提示使用者輸入連線資訊
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f52e0d120fb150fe58b850107847d7ef5df20e7c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465710"
---
# <a name="prompting-the-user-for-connection-information"></a>提示使用者輸入連線資訊
如果應用程式使用 **SQLConnect** ，且需要提示使用者輸入任何連接資訊（例如使用者名稱和密碼），則必須自行進行。 雖然這可讓應用程式控制其「外觀及操作」，但它可能會強制應用程式包含驅動程式特定的程式碼。 當應用程式需要提示使用者提供驅動程式特定的連接資訊時，就會發生這種情況。 這是一般應用程式的不可能情況，其設計目的是要使用任何和所有驅動程式，包括寫入應用程式時不存在的驅動程式。  
  
 **SQLDriverConnect** 可以提示使用者輸入連接資訊。 例如，先前提及的自訂程式可能會將下列連接字串傳遞至 **SQLDriverConnect**：  
  
```  
DSN=XYZ Corp;  
```  
  
 然後，驅動程式可能會顯示一個對話方塊，提示您輸入使用者識別碼和密碼，如下圖所示。  
  
 ![提示輸入使用者 ID 與密碼的對話方塊](../../../odbc/reference/develop-app/media/pr18.gif "pr18")  
  
 驅動程式可能會提示您輸入連線資訊，對於一般和垂直應用程式來說特別有用。 這些應用程式不應包含驅動程式專屬的資訊，並讓驅動程式提示您輸入所需的資訊會將該資訊保留在應用程式外。 這會顯示在前兩個範例中。 當應用程式只將資料來源名稱傳遞至驅動程式時，應用程式不會包含任何驅動程式特定的資訊，因此不會系結至特定的驅動程式。 當應用程式將完整的連接字串傳遞至驅動程式時，它會系結至可能解讀該字串的驅動程式。  
  
 泛型應用程式可能會進一步執行這個步驟，甚至不會指定資料來源。 當 **SQLDriverConnect** 收到空的連接字串時，驅動程式管理員會顯示下列對話方塊。  
  
 ![[選取資料來源] 對話方塊](../../../odbc/reference/develop-app/media/ch06a.gif "CH06A")  
  
 當使用者選取資料來源之後，驅動程式管理員會建立指定該資料來源的連接字串，並將它傳遞至驅動程式。 然後，驅動程式會提示使用者提供所需的任何其他資訊。  
  
 驅動程式提示使用者的條件是由 *DriverCompletion* 旗標控制;有一些選項可一律提示、必要時提示，或永遠不提示。 如需此旗標的完整描述，請參閱 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) 函數描述。
