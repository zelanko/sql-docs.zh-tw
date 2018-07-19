---
title: 參照 ADO 程式庫中的 Visual c + + 應用程式 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- libraries [ADO]
- referencing libraries in a Visual C++ application[ADO]
- ADO, libraries
ms.assetid: d3ea12ec-bca8-48c3-af57-ce14576108c9
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6a38e5df65def060668e60ee470dc379b873ab35
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/11/2018
ms.locfileid: "35273607"
---
# <a name="referencing-the-ado-libraries-in-a-visual-c-application"></a>參照 ADO 程式庫中的 Visual c + + 應用程式
若要使用 ADO 的最新版本的 Visual c + + 應用程式中，使用下列`#import`指示詞：  
  
```  
#import "msado15.dll" \  
    no_namespace rename("EOF", "EndOfFile")  
```  
  
 若要使用 ADO MD 或 ADOX，您必須匯入*msadomd.dll*或*msadox.dll*，可以使用上述語法。  
  
## <a name="backward-compatibility"></a>Backward Compatibility  
 若要使用 ADO 的任何先前的版本，取代*msado15.dll*上面其中下列型別程式庫。  
  
-   *msado27.tlb*，ADO 2.7 類型程式庫  
  
-   *msado26.tlb*，ADO 2.6 類型程式庫  
  
-   *msado25.tlb*，ADO 2.5 的型別程式庫  
  
-   *msado21.tlb*，ADO 2.1 的型別程式庫  
  
-   *msado20.tlb*，ADO 2.0 類型程式庫
