---
description: Visual C++ Extensions for ADO
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
ms.openlocfilehash: f9fa962d4710811cf376634dcc299707f6b0e654
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88453930"
---
# <a name="visual-c-extensions-for-ado"></a>Visual C++ Extensions for ADO
使用 Visual C++ 的 ADO 程式設計慣用方法，是使用 **#import** 指示詞，如 [Microsoft Visual C++ ADO 程式設計](../../../ado/guide/appendixes/visual-c-ado-programming.md)中所述。 不過，舊版 ADO 隨附的替代方法是使用 Visual C++： Visual C++ 擴充功能。 本節說明必須維護 Visual C++ 擴充程式碼的這項功能，但應該使用 #**import**來撰寫新的 ADO 程式碼。

 在程式設計人員使用 ADO 抓取資料時，最繁瑣的 Visual C++ 工作之一，就是將傳回為 VARIANT 資料類型的資料轉換成 c + + 資料類型，然後將轉換的資料儲存在類別或結構中。 除了麻煩，透過 VARIANT 資料類型來抓取 c + + 資料也會降低效能。

 ADO 提供一個介面，可支援將資料移至原生 C/c + + 資料類型，而不需經過變異數，而且也提供可簡化使用介面的預處理器宏。 結果是一種彈性的工具，可讓您更輕鬆地使用並提供絕佳的效能。

 常見的 C/c + + 用戶端案例是將記錄 [集](../../../ado/reference/ado-api/recordset-object-ado.md) 內的記錄系結至 C/c + + 結構或包含原生 C/c + + 類型的類別。 當您完成變化時，這牽涉到將轉換程式碼從 VARIANT 寫入至 C/c + + 原生類型。 適用于 ADO 的 Visual C++ 延伸模組的目標是讓 Visual C++ 程式設計人員更容易進行此案例。

 請參閱下列主題，以深入瞭解適用于 ADO 的 Visual C++ 延伸模組。

-   [使用 Visual C++ 的 ADO 延伸模組](../../../ado/guide/appendixes/using-visual-c-extensions.md)

-   [Visual C++ Extensions 標題](../../../ado/guide/appendixes/visual-c-extensions-header.md)

-   [具有 Visual C++ 擴充功能的 ADO 範例](../../../ado/guide/appendixes/visual-c-extensions-example.md)

## <a name="see-also"></a>另請參閱
 [使用 Visual C++ 延伸模組](../../../ado/guide/appendixes/using-visual-c-extensions.md) [Visual C++ 延伸模組標頭](../../../ado/guide/appendixes/visual-c-extensions-header.md)的 Visual C++ COM [Visual C++ 擴充功能範例](../../../ado/guide/appendixes/visual-c-extensions-example.md)[的語法索引 ADO](../../../ado/reference/ado-api/ado-for-visual-c-syntax-index-for-com.md)
