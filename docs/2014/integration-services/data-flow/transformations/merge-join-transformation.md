---
title: 合併聯結轉換 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.mergejointrans.f1
helpviewer_keywords:
- datasets [Integration Services]
- Merge Join transformation
- datasets [Integration Services], joining
- joining datasets [Integration Services]
- joins [SQL Server], SSIS
ms.assetid: cd8b0412-f83b-4bd2-b227-e53dcfd941a8
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 0ef70f4f9d28fc23c0ac0a168447cc1b8867cd27
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62900164"
---
# <a name="merge-join-transformation"></a>Merge Join Transformation
  合併聯結轉換提供藉由使用 FULL、LEFT 或 INNER 聯結，來聯結兩個已排序資料集所產生的輸出。 例如，您可以使用 LEFT 聯結來聯結包含產品資訊的資料表，以及列出製造產品的國家/地區的資料表。 此結果為列出所有產品及其原產國家/地區的資料表。  
  
 您可以利用下列方式設定「合併聯結」轉換：  
  
-   指定聯結為 FULL、LEFT 或 INNER 聯結。  
  
-   指定聯結使用的資料行。  
  
-   指定轉換是否要將 Null 值當作相當於其他 Null 處理。  
  
    > [!NOTE]  
    >  如果 Null 值未當成相等值，則轉換會以與 SQL Server Database Engine 相同的方式處理 Null 值。  
  
 這個轉換有兩個輸入與一個輸出。 它不支援錯誤輸出。  
  
## <a name="input-requirements"></a>輸入需求  
 合併聯結轉換針對其輸入需要已排序的資料。 如需這項重要需求的詳細資訊，請參閱 [排序合併和合併聯結轉換的資料](sort-data-for-the-merge-and-merge-join-transformations.md)。  
  
## <a name="join-requirements"></a>聯結需求  
 合併聯結轉換會要求聯結的資料行擁有相符的中繼資料。 例如，您無法聯結數值資料類型的資料行，與字元資料類型的資料行。 如果資料是字串資料類型，第二個輸入中的資料行長度就必須小於或等於與其合併之第一個輸入中的資料行長度。  
  
## <a name="buffer-throttling"></a>緩衝區調整  
 您再也不必設定 `MaxBuffersPerInput` 屬性的值，因為 Microsoft 已做出變更，降低合併聯結轉換會耗用過多記憶體的風險。 這個問題有時候會發生在合併聯結的多個輸入以不平均的速率產生資料時。  
  
## <a name="related-tasks"></a>相關工作  
 您可以透過「 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師」或以程式設計方式設定屬性。  
  
 如需有關如何設定此轉換屬性的詳細資訊，請按下列其中一個主題：  
  
-   [使用合併聯結轉換來擴充資料集](merge-join-transformation.md)  
  
-   [設定資料流程元件的屬性](../set-the-properties-of-a-data-flow-component.md)  
  
-   [排序合併和合併聯結轉換的資料](sort-data-for-the-merge-and-merge-join-transformations.md)  
  
## <a name="see-also"></a>另請參閱  
 [合併聯結轉換編輯器](../../merge-join-transformation-editor.md)   
 [合併轉換](merge-transformation.md)   
 [聯集全部轉換](union-all-transformation.md)   
 [Integration Services 轉換](integration-services-transformations.md)  
  
  
