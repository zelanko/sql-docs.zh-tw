---
title: 視覺化C++延伸模組用於 ADO |Microsoft Docs
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
manager: jroth
ms.openlocfilehash: ccd783bdb7bf266bfdc83c3a02520345d707ceea
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2019
ms.locfileid: "66702629"
---
# <a name="visual-c-extensions-for-ado"></a>Visual C++ Extensions for ADO
慣用的程式設計視覺效果的 ADO 方法C++使用 **#import**指示詞中所述[Microsoft Visual C++ ADO 程式設計](../../../ado/guide/appendixes/visual-c-ado-programming.md)。 不過，舊版 ADO 隨附程式設計使用視覺效果的替代方法C++： 視覺效果C++延伸模組。 本節提供這項功能的人必須維護視覺效果C++擴充功能的程式碼，但新的 ADO 程式碼應該使用來撰寫 #**匯入**。

 其中一個最沉悶作業 VisualC++程式設計人員臉部 ADO 使用擷取資料時將資料轉換時傳回當做 VARIANT 資料類型到C++資料類型，然後將轉換的資料儲存在類別或結構。 除了很麻煩，擷取C++透過 VARIANT 資料類型的資料會減少效能。

 ADO 提供的介面，支援資料擷取到原生 C /C++資料類型而不需要經過 VARIANT，同時也提供 前置處理器巨集，可簡化使用介面。 結果是有彈性的工具更容易使用且具有極佳的效能。

 常見的 C /C++用戶端的案例是要繫結中的資料錄[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)之 c /C++結構或類別，包含原生 C /C++類型。 透過變數時，這牽涉到從 VARIANT 轉換程式碼寫入 C /C++原生型別。 視覺效果C++延伸模組用於 ADO 為目標的視覺效果，讓這個案例更容易C++程式設計人員。

 請參閱下列主題來深入了解視覺效果C++延伸模組用於 ADO。

-   [使用視覺效果C++延伸模組用於 ADO](../../../ado/guide/appendixes/using-visual-c-extensions.md)

-   [Visual C++ Extensions 標題](../../../ado/guide/appendixes/visual-c-extensions-header.md)

-   [ADO 使用 VisualC++延伸模組範例](../../../ado/guide/appendixes/visual-c-extensions-example.md)

## <a name="see-also"></a>另請參閱
 [ADO for VisualC++語法索引 com](../../../ado/reference/ado-api/ado-for-visual-c-syntax-index-for-com.md) [視覺化C++延伸模組範例](../../../ado/guide/appendixes/visual-c-extensions-example.md)[使用視覺效果C++延伸模組](../../../ado/guide/appendixes/using-visual-c-extensions.md) [VisualC++延伸模組標頭](../../../ado/guide/appendixes/visual-c-extensions-header.md)
