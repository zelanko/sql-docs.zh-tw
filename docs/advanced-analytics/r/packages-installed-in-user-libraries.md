---
title: "安裝在使用者程式庫中的封裝 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 99ffd9b8-aa6d-4ac2-9840-4e66d0463978
caps.latest.revision: 2
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b4d5c7f3d1d0da5e1967140fcbdfcf60ba4571e7
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="packages-installed-in-user-libraries"></a>安裝在使用者程式庫中的封裝

如果使用者需要新的 R 封裝且不是系統管理員，就無法將封裝安裝到預設位置，而是會依預設安裝到私用的使用者程式庫。 

在一般的 R 開發環境中，若要在程式碼中參考封裝，使用者必須將位置加入至 R 環境變數 `libPath`，或參考完整的封裝路徑，就像這樣：  
  
~~~~
library("c:/Users/<username>/R/win-library/packagename")  
~~~~

## <a name="problems-with-packages-in-user-libraries"></a>使用者程式庫中的封裝問題

不過，在 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 中，不支援這個因應措施；必須將封裝安裝到預設程式庫。 如果封裝並未安裝於預設程式庫中，您可能會在嘗試呼叫封裝時發生這個錯誤：

程式庫(xxx) 中發生錯誤︰沒有名為 'xxx' 的封裝
 

因此，當您移轉要在 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 中執行的 R 方案時，請務必執行下列動作：
+ 將任何您需要的封裝安裝到預設程式庫。
+ 編輯程式碼，以確定封裝是從預設程式庫載入，而不是從特定的目錄或使用者程式庫載入。
+ 檢查您的程式碼，以確保不會呼叫已解除安裝的封裝。
+ 修改任何會嘗試以動態方式安裝封裝的程式碼。
 
如果已將封裝安裝於預設程式庫中，R 執行階段將從預設程式庫載入封裝，即使已在 R 程式碼中指定不同的程式庫也一樣。

## <a name="see-also"></a>另請參閱
