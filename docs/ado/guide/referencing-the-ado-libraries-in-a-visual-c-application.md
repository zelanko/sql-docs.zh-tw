---
title: 參照 ADO 程式庫中的 Visual c + + 應用程式 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology: drivers
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
ms.workload: Inactive
ms.openlocfilehash: a8053304a845eefbe51b1c24221a063cf4496679
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/18/2018
---
# <a name="referencing-the-ado-libraries-in-a-visual-c-application"></a>參照 ADO 程式庫中的 Visual c + + 應用程式
若要使用 ADO 的最新版本的 Visual c + + 應用程式中，使用下列`#import`指示詞：  
  
```  
#import "msado15.dll" \  
    no_namespace rename("EOF", "EndOfFile")  
```  
  
 若要使用 ADO MD 或 ADOX，您必須匯入*msadomd.dll*或*msadox.dll*，可以使用上述語法。  
  
## <a name="backward-compatibility"></a>回溯相容性  
 若要使用 ADO 的任何先前的版本，取代*msado15.dll*上面其中下列型別程式庫。  
  
-   *msado27.tlb*，ADO 2.7 類型程式庫  
  
-   *msado26.tlb*，ADO 2.6 類型程式庫  
  
-   *msado25.tlb*，ADO 2.5 的型別程式庫  
  
-   *msado21.tlb*，ADO 2.1 的型別程式庫  
  
-   *msado20.tlb*，ADO 2.0 類型程式庫
