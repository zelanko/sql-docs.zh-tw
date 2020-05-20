---
title: 在 Visual C++ 應用程式中參考 ADO 程式庫 |Microsoft Docs
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- libraries [ADO]
- referencing libraries in a Visual C++ application[ADO]
- ADO, libraries
ms.assetid: d3ea12ec-bca8-48c3-af57-ce14576108c9
author: rothja
ms.author: jroth
ms.openlocfilehash: a790ace40aa31324ce8b22127d8f6948ae86e059
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82764759"
---
# <a name="referencing-the-ado-libraries-in-a-visual-c-application"></a>在 Visual C++ 應用程式中參考 ADO 程式庫
若要在 Visual C++ 應用程式中使用最新版本的 ADO，請使用下列指示詞 `#import` ：  
  
```cpp
#import "msado15.dll" \  
    no_namespace rename("EOF", "EndOfFile")  
```  
  
 若要使用 ADO MD 或 ADOX，您必須使用上述語法匯入*msadomd .dll*或*msadox*。  
  
## <a name="backward-compatibility"></a>回溯相容性  
 若要使用任何舊版的 ADO，請將上述的 msado15.dll 取代為下列其中一個類型*連結*庫。  
  
-   *msado27 .tlb*、ADO 2.7 類型程式庫  
  
-   *msado26 .tlb*、ADO 2.6 類型程式庫  
  
-   *msado25 .tlb*、ADO 2.5 類型程式庫  
  
-   *msado21 .tlb*、ADO 2.1 類型程式庫  
  
-   *msado20 .tlb*、ADO 2.0 類型程式庫
