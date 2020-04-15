---
title: 提示使用者輸入連線資訊 |微軟文件
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
ms.openlocfilehash: 9b0f120a1076f14f5e67d506e52a446e0a3d4713
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81282081"
---
# <a name="prompting-the-user-for-connection-information"></a>提示使用者輸入連線資訊
如果應用程式使用**SQLConnect,** 並且需要提示使用者輸入任何連接資訊(如使用者名和密碼),則必須自行執行此操作。 雖然這允許應用程式控制其"外觀",但它可能會強制應用程式包含特定於驅動程序的代碼。 當應用程式需要提示使用者輸入特定於驅動程式的連接資訊時,將發生這種情況。 這給通用應用程式帶來了一個不可能的情況,這些驅動程式旨在處理任何和所有驅動程式,包括編寫應用程式時不存在的驅動程式。  
  
 **SQLDriverConnect**可以提示使用者提供連接資訊。 例如,前面提到的自訂程式可以將以下連接字串傳遞給**SQLDriverConnect**:  
  
```  
DSN=XYZ Corp;  
```  
  
 然後,驅動程式可能會顯示一個對話框,提示使用者使用I和密碼,類似於下圖。  
  
 ![提示輸入使用者 ID 與密碼的對話方塊](../../../odbc/reference/develop-app/media/pr18.gif "pr18")  
  
 驅動程式可以提示連接資訊對於通用和垂直應用程式特別有用。 這些應用程式不應包含特定於驅動程式的資訊,並且讓驅動程式提示它需要的資訊會將該資訊從應用程式中排除。 這由前兩個示例顯示。 當應用程式僅將資料源名稱傳遞給驅動程式時,應用程式不包含任何特定於驅動程序的資訊,因此不綁定到特定驅動程式。 當應用程式將完整的連接字串傳遞給驅動程式時,它綁定到可以解釋該字串的驅動程式。  
  
 泛型應用程式可能會更進一步,甚至不會指定數據源。 當**SQLDriverConnect**收到空連接字串時,驅動程式管理器將顯示以下對話框。  
  
 ![[選取資料來源] 對話方塊](../../../odbc/reference/develop-app/media/ch06a.gif "CH06A")  
  
 用戶選擇數據源後,驅動程式管理器將建構一個連接字串,指定該數據源並將其傳遞給驅動程式。 然後,驅動程式可以提示使用者提供所需的任何其他資訊。  
  
 驅動程式提示用戶的條件由*驅動程式完成*標誌控制;有選項可以始終提示、在必要時提示或從不提示。 有關此標誌的完整說明,請參閱[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)函數說明。
