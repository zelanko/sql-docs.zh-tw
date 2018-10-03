---
title: Visual c + + 延伸模組用於 ADO |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
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
ms.openlocfilehash: ca21e976783a10a738488762e382982e4fd8fd8a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47747676"
---
# <a name="visual-c-extensions"></a>Visual c + + 延伸模組
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
