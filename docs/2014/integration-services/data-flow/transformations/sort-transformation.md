---
title: 排序轉換 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.sorttrans.f1
helpviewer_keywords:
- Sort transformation
- descending sorts
- ascending sorts
- sorting data [Integration Services]
- multiple sorts
- duplicate data [Integration Services]
ms.assetid: 728c9351-84a8-4a89-be4d-d50d4adc04e0
caps.latest.revision: 50
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 5155e1bc61e5a02d29420d20b1e2970693dda1da
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37150719"
---
# <a name="sort-transformation"></a>排序轉換
  「排序」轉換會以遞增或遞減的順序排序輸入資料，並將排序的資料複製到轉換輸出。 您可以對輸入套用多項排序，而各項排序是由決定排序順序的數字識別。 數字最小的資料行會最先排序，接著是排序數字第二小的排序資料行，以此類推。 例如，如果名為 **CountryRegion** 的資料行排序順序為 1，且名為 **City** 的資料行排序順序為 2，則輸出會先按照 Country/Region 排序，然後才按照 City。 正數代表以遞增順序排序，負數則代表以遞減順序排序。 未排序的資料行具有 0 的排序次序。 未選取進行排序的資料行會與經過排序的資料行一起自動複製到轉換輸出。  
  
 「排序」轉換包括一組比較選項，用來定義轉換處理資料行中字串資料的方式。 如需詳細資訊，請參閱 [Comparing String Data](../comparing-string-data.md)。  
  
> [!NOTE]  
>  「排序」轉換排序 GUID 時，與 ORDER BY 子句在 Transact-SQL 中排序的方式不同。 「排序」轉換會排序以 A-F 開頭之 GUID 前，以 0-9 開頭的 GUID，而在 [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)] 中實作的 ORDER BY 子句則以不同的方式排序。 如需詳細資訊，請參閱 [ORDER BY 子句 &#40;Transact-SQL&#41;](/sql/t-sql/queries/select-order-by-clause-transact-sql)。  
  
 「排序」轉換亦可在執行排序時移除重複的資料列。 重複的資料列為擁有相同排序索引鍵值的資料列。 排序索引鍵值是根據使用的字串比較選項所產生，也就是說，不同的常值字串可能擁有相同的排序索引鍵值。 轉換會將輸入資料行中，擁有不同值但排序索引鍵相同的資料列視為重複。  
  
 「 排序 」 轉換包含`MaximumThreads`載入封裝時可以更新屬性運算式的自訂屬性。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 運算式](../../expressions/integration-services-ssis-expressions.md)、[在封裝中使用屬性運算式](../../expressions/use-property-expressions-in-packages.md)和[轉換自訂屬性](transformation-custom-properties.md)。  
  
 此轉換有一個輸入和一個輸出。 但它不支援錯誤輸出。  
  
## <a name="configuration-of-the-sort-transformation"></a>設定排序轉換  
 您可以透過「 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師」或以程式設計方式設定屬性。  
  
 如需有關 **[排序轉換編輯器]** 對話方塊中可設定屬性的詳細資訊，請參閱＜ [Sort Transformation Editor](../../sort-transformation-editor.md)＞。  
  
 **[進階編輯器]** 對話方塊會反映能以程式設計的方式設定之屬性。 如需有關可以在 **[進階編輯器]** 對話方塊中或以程式設計方式設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [通用屬性](../../common-properties.md)  
  
-   [轉換自訂屬性](transformation-custom-properties.md)  
  
## <a name="related-tasks"></a>相關工作  
 如需如何設定元件屬性的詳細資訊，請參閱 [設定資料流程元件的屬性](../set-the-properties-of-a-data-flow-component.md)。  
  
## <a name="related-content"></a>相關內容  
 codeplex.com 上的範例： [SortDeDuplicateDelimitedString 自訂 SSIS 元件](http://go.microsoft.com/fwlink/?LinkId=220821)。  
  
## <a name="see-also"></a>另請參閱  
 [資料流程](../data-flow.md)   
 [Integration Services 轉換](integration-services-transformations.md)  
  
  
