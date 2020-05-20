---
title: 適用于 ADO 的 Visual C++ 延伸模組 |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: f623bd3eb0c0c4cdde47c6fea7e7cd8af2ad0de6
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82761516"
---
# <a name="visual-c-extensions-for-ado"></a>Visual C++ Extensions for ADO
採用 Visual C++ 的 ADO 程式設計的慣用方法是使用 **#import**指示詞，如[Microsoft Visual C++ ADO 程式設計](../../../ado/guide/appendixes/visual-c-ado-programming.md)中所述。 不過，舊版 ADO 隨附另一個使用 Visual C++ 的程式設計方法： Visual C++ 延伸模組。 本節會針對必須維護 Visual C++ 延伸模組程式碼的人員記載這項功能，但新的 ADO 程式碼應使用 #**import**來撰寫。

 Visual C++ 程式設計人員在使用 ADO 來抓取資料時最繁瑣的工作之一，就是將傳回為 VARIANT 資料類型的資料轉換成 c + + 資料類型，然後將轉換的資料儲存在類別或結構中。 除了麻煩外，透過 VARIANT 資料類型來抓取 c + + 資料也會降低效能。

 ADO 提供的介面可支援在不經過變體的情況下，將資料抓取至原生 C/c + + 資料類型，同時也提供可簡化使用介面的預處理器宏。 結果是彈性的工具，更容易使用且具有良好的效能。

 常見的 C/c + + 用戶端案例是將記錄[集](../../../ado/reference/ado-api/recordset-object-ado.md)內的記錄系結至 c/c + + 結構或包含原生 C/c + + 類型的類別。 透過變體時，這牽涉到將轉換程式碼從 VARIANT 寫成 C/c + + 原生類型。 ADO 的 Visual C++ 延伸模組的目標在於讓 Visual C++ 程式設計人員更容易進行這個案例。

 若要深入瞭解 ADO 的 Visual C++ 延伸模組，請參閱下列主題。

-   [使用 ADO 的 Visual C++ 延伸模組](../../../ado/guide/appendixes/using-visual-c-extensions.md)

-   [Visual C++ Extensions 標題](../../../ado/guide/appendixes/visual-c-extensions-header.md)

-   [具有 Visual C++ 擴充功能的 ADO 範例](../../../ado/guide/appendixes/visual-c-extensions-example.md)

## <a name="see-also"></a>另請參閱
 適用于 COM [Visual C++ 延伸模組範例](../../../ado/guide/appendixes/visual-c-extensions-example.md) [Visual C++ 語法索引的 ADO](../../../ado/reference/ado-api/ado-for-visual-c-syntax-index-for-com.md) [Visual C++ 延伸模組標頭](../../../ado/guide/appendixes/visual-c-extensions-header.md)[使用 Visual C++ 延伸](../../../ado/guide/appendixes/using-visual-c-extensions.md)模組
