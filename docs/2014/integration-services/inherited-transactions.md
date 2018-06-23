---
title: 繼承的交易 |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- transactions [Integration Services], inherited
- child packages
- inherited transactions [Integration Services]
ms.assetid: 90db5564-d41e-4cfe-8c9e-4e68d41eff1c
caps.latest.revision: 34
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 0df0ba113b23e9b5cc582b1795299a0befee4bae
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36133300"
---
# <a name="inherited-transactions"></a>繼承的交易
  封裝可使用「執行封裝」工作執行另一個封裝。 子封裝 (亦即「執行封裝」工作所執行的封裝) 可建立其自己的封裝交易，也可以繼承父封裝交易。  
  
 如果下列兩個情況均成立，則子封裝將會繼承父封裝交易：  
  
-   由一「執行封裝」工作叫用 (Invoke) 該封裝。  
  
-   叫用該封裝的「執行封裝」工作亦聯結父封裝交易。  
  
 除非子封裝自行聯結交易，否則子封裝中的容器和工作無法聯結父封裝交易。  
  
## <a name="illustration-of-package-transactions"></a>封裝交易的圖例說明  
 在下圖中，有三個使用交易的封裝。 每一個封裝都包含多個工作。 為強調交易的行為，只會顯示「執行封裝」工作。 封裝 A 執行封裝 B 和 C。而封裝 B 又執行封裝 D 和 E，封裝 C 執行封裝 F。  
  
 封裝和工作具有下列交易屬性：  
  
-   在封裝 A 和 C 上，**TransactionOption** 設為 **Required**   
  
-   在封裝 B 和 D 上，以及在「執行封裝 B」、「執行封裝 D」和「執行封裝 F」工作上，**TransactionOption** 設為 **Supported** 。  
  
-   在封裝 E 上，以及在「執行封裝 C」和「執行封裝 E」工作上，**TransactionOption** 設為 **NotSupported** 。  
  
 ![繼承的交易流程](media/mw-dts-executepack.gif "繼承的交易流程")  
  
 只有封裝 B、D 和 F 可從其父封裝繼承交易。  
  
 封裝 B 和 D 會繼承由封裝 A 啟動的交易。  
  
 封裝 F 會繼承由封裝 C 啟動的交易。  
  
 封裝 A 和 C 會控制其自己的交易。  
  
 封裝 E 不使用交易。  
  
## <a name="related-tasks"></a>相關工作  
 [封裝設定成使用交易](../relational-databases/native-client-ole-db-transactions/transactions.md)  
  
  