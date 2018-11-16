---
title: Visual c + + 延伸模組用於 ADO |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- ADO, Visual C++
- Visual C++ [ADO], VC++ extensions for ADO
ms.assetid: 2952ece0-7217-4448-bb09-f6b64f43b7e2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4432c125b0c860775911aa753984806a472a64ba
ms.sourcegitcommit: 96b2355d54dfad259826e88bdff91cc9344e16f2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2018
ms.locfileid: "51350183"
---
# <a name="visual-c-extensions-for-ado"></a>Visual C++ Extensions for ADO
程式設計 Visual c + + ADO 的慣用的方法使用 **#import**指示詞中所述[Microsoft Visual c + + ADO 程式設計](../../../ado/guide/appendixes/visual-c-ado-programming.md)。 不過，舊版 ADO 隨附使用 Visual c + + 的程式設計替代方法： Visual c + + 延伸模組。 本節提供這項功能的人必須維護 Visual c + + 延伸模組的程式碼，但新的 ADO 程式碼應該使用 # 來撰寫**匯入**。

 其中一個最沉悶作業 Visual c + + 程式設計人員所面臨的 ADO 使用擷取資料會轉換成 c + + 資料型別，傳回 VARIANT 資料類型，而然後將轉換的資料儲存在類別或結構的資料時。 除了很麻煩，擷取透過 VARIANT 資料類型的 c + + 資料減少效能。

 ADO 提供的介面，支援擷取資料到原生 C/c + + 資料類型，而不需要經過 VARIANT，並提供簡化使用介面的前置處理器巨集。 結果是有彈性的工具更容易使用且具有極佳的效能。

 常見的 C/c + + 用戶端案例是要繫結中的資料錄[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)C/c + + 結構或類別，包含原生 C/c + + 類型。 透過變數時，這牽涉到從 VARIANT 轉換程式碼寫入 C/c + + 原生型別。 Visual c + + 延伸模組，用於 ADO 為目標的 Visual c + + 程式設計師，使得這種情況下更為簡單。

 請參閱下列主題來深入了解 Visual c + + 延伸模組，用於 ADO。

-   [ADO 使用 Visual c + + 延伸模組](../../../ado/guide/appendixes/using-visual-c-extensions.md)

-   [Visual C++ Extensions 標題](../../../ado/guide/appendixes/visual-c-extensions-header.md)

-   [ADO 使用 Visual c + + 延伸模組範例](../../../ado/guide/appendixes/visual-c-extensions-example.md)

## <a name="see-also"></a>另請參閱
 [Visual c + + 語法索引 com 的 ADO](../../../ado/reference/ado-api/ado-for-visual-c-syntax-index-for-com.md) [Visual c + + Extensions 範例](../../../ado/guide/appendixes/visual-c-extensions-example.md)[使用 Visual c + + 擴充功能](../../../ado/guide/appendixes/using-visual-c-extensions.md) [Visual c + + Extensions 標題](../../../ado/guide/appendixes/visual-c-extensions-header.md)
