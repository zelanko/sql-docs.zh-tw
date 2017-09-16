---
title: "Visual c + + 延伸模組用於 ADO |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: H1Hack27Feb2017
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- C++
helpviewer_keywords:
- ADO, Visual C++
- Visual C++ [ADO], VC++ extensions for ADO
ms.assetid: 2952ece0-7217-4448-bb09-f6b64f43b7e2
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: fbc17b15d552f9b7afeeb4841febdd7d08e54808
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="visual-c-extensions"></a>Visual c + + 擴充功能
程式設計 Visual c + + 的 ADO 的慣用的方法使用**#import**指示詞中所述[Microsoft Visual c + + ADO Programming](../../../ado/guide/appendixes/visual-c-ado-programming.md)。 不過，舊版的 ADO 隨附的 Visual c + + 的程式設計替代方法： Visual c + + 擴充功能。 本章節記載這項功能的人員必須維護 Visual c + + 擴充功能的程式碼，但新的 ADO 程式碼應該使用 # 來撰寫**匯入**。

 面臨的其中一個最繁瑣作業 Visual c + + 程式設計人員使用 ADO 來擷取資料會轉換成 c + + 資料類型，當做 VARIANT 資料類型傳回，而且然後儲存轉換的資料類別或結構中的資料時。 除了麻煩，擷取透過 VARIANT 資料類型的 c + + 資料減少效能。

 ADO 提供的介面，支援擷取資料到原生 C/c + + 資料類型，而不需要透過 VARIANT，並提供前置處理器巨集，可簡化使用介面中。 結果是有彈性的工具更容易使用且具有較佳的效能。

 一般的 C/c + + 用戶端案例是將繫結中的記錄[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)C/c + + 結構或類別包含原生 C/c + + 類型。 當經過變體，這牽涉到從 VARIANT 轉換程式碼寫入 C/c + + 原生類型。 ADO 的 Visual c + + 擴充功能的適用對象為 Visual c + + 程式設計人員，使得此案例中更為簡單。

 請參閱下列主題來深入了解 ADO 的 Visual c + + 擴充功能。

-   [針對 ADO 使用 Visual c + + 擴充功能](../../../ado/guide/appendixes/using-visual-c-extensions.md)

-   [Visual c + + 擴充功能的標頭](../../../ado/guide/appendixes/visual-c-extensions-header.md)

-   [ADO 使用 Visual c + + 擴充功能範例](../../../ado/guide/appendixes/visual-c-extensions-example.md)

## <a name="see-also"></a>另請參閱
 [Visual c + + 語法索引 com ADO](../../../ado/reference/ado-api/ado-for-visual-c-syntax-index-for-com.md) [Visual c + + 擴充功能範例](../../../ado/guide/appendixes/visual-c-extensions-example.md)[使用 Visual c + + 擴充功能](../../../ado/guide/appendixes/using-visual-c-extensions.md) [Visual c + + 擴充功能的標頭](../../../ado/guide/appendixes/visual-c-extensions-header.md)

