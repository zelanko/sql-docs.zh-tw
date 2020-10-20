---
description: 排序轉換
title: 排序轉換 | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.sorttrans.f1
- sql13.dts.designer.sorttransformation.f1
helpviewer_keywords:
- Sort transformation
- descending sorts
- ascending sorts
- sorting data [Integration Services]
- multiple sorts
- duplicate data [Integration Services]
ms.assetid: 728c9351-84a8-4a89-be4d-d50d4adc04e0
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 7830dbd1bcb5daf81234a6948b13effc37a3b46b
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/19/2020
ms.locfileid: "92195932"
---
# <a name="sort-transformation"></a>排序轉換

[!INCLUDE[sqlserver-ssis](../../../includes/applies-to-version/sqlserver-ssis.md)]


  「排序」轉換會以遞增或遞減的順序排序輸入資料，並將排序的資料複製到轉換輸出。 您可以對輸入套用多項排序，而各項排序是由決定排序順序的數字識別。 數字最小的資料行會最先排序，接著是排序數字第二小的排序資料行，以此類推。 例如，如果名為 **CountryRegion** 的資料行排序順序為 1，且名為 **City** 的資料行排序順序為 2，則輸出會先按照 Country/Region 排序，然後才按照 City。 正數代表以遞增順序排序，負數則代表以遞減順序排序。 未排序的資料行具有 0 的排序次序。 未選取進行排序的資料行會與經過排序的資料行一起自動複製到轉換輸出。  
  
 「排序」轉換包括一組比較選項，用來定義轉換處理資料行中字串資料的方式。 如需詳細資訊，請參閱 [Comparing String Data](../../../integration-services/data-flow/comparing-string-data.md)。  
  
> [!NOTE]  
>  「排序」轉換排序 GUID 時，與 ORDER BY 子句在 Transact-SQL 中排序的方式不同。 「排序」轉換會排序以 A-F 開頭之 GUID 前，以 0-9 開頭的 GUID，而在 [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)]中實作的 ORDER BY 子句則以不同的方式排序。 如需詳細資訊，請參閱 [ORDER BY 子句 &#40;Transact-SQL&#41;](../../../t-sql/queries/select-order-by-clause-transact-sql.md)。  
  
 「排序」轉換亦可在執行排序時移除重複的資料列。 重複的資料列為擁有相同排序索引鍵值的資料列。 排序索引鍵值是根據使用的字串比較選項所產生，也就是說，不同的常值字串可能擁有相同的排序索引鍵值。 轉換會將輸入資料行中，擁有不同值但排序索引鍵相同的資料列視為重複。  
  
 排序轉換包括 **MaximumThreads** 自訂屬性；屬性運算式可以在載入封裝時更新這個屬性。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 運算式](../../../integration-services/expressions/integration-services-ssis-expressions.md)、[在封裝中使用屬性運算式](../../../integration-services/expressions/use-property-expressions-in-packages.md)和[轉換自訂屬性](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)。  
  
 此轉換有一個輸入和一個輸出。 但它不支援錯誤輸出。  
  
## <a name="configuration-of-the-sort-transformation"></a>設定排序轉換  
 您可以透過「 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師」或以程式設計方式設定屬性。  
  
 **[進階編輯器]** 對話方塊會反映能以程式設計的方式設定之屬性。 如需有關可以在 **[進階編輯器]** 對話方塊中或以程式設計方式設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [Common Properties](../set-the-properties-of-a-data-flow-component.md)  
  
-   [轉換自訂屬性](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
## <a name="related-tasks"></a>相關工作  
 如需如何設定元件屬性的詳細資訊，請參閱 [設定資料流程元件的屬性](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)。  
  
## <a name="related-content"></a>相關內容  
 codeplex.com 上的範例： [SortDeDuplicateDelimitedString 自訂 SSIS 元件](https://go.microsoft.com/fwlink/?LinkId=220821)。  
  
## <a name="sort-transformation-editor"></a>排序轉換編輯器
  使用 **[排序轉換編輯器]** 對話方塊，即可選取要排序的資料行、設定排序順序和指定是否要移除重複的項目。  
  
### <a name="options"></a>選項。  
 **可用的輸入資料行**  
 使用核取方塊來指定要排序的資料行。  
  
 **名稱**  
 檢視每個可用輸入資料行的名稱。  
  
 **通過**  
 指出排序的輸出中是否包含資料行。  
  
 **輸入資料行**  
 從每個資料列的可用輸入資料行清單中選取。 您的選擇會反映在 **[可用的輸入資料行]** 資料表的核取方塊選擇中。  
  
 **輸出別名**  
 輸入每一個輸出資料行的別名。 預設是輸入資料行的名稱；但是，您可以選擇任何唯一的、描述性名稱。  
  
 **排序類型**  
 指出是要依遞增或遞減的順序來排序。  
  
 **排序次序**  
 指出資料行的排序順序。 必須以手動的方式為每個資料行設定。  
  
 **比較旗標**  
 如需字串比較選項的資訊，請參閱 [比較字串資料](../../../integration-services/data-flow/comparing-string-data.md)。  
  
 **移除排序值重複的資料列**  
 指出轉換是否將重複的資料列複製到轉換輸出，或依據指定的字串比較選項為所有重複的資料列建立單一項目。  
  
## <a name="see-also"></a>另請參閱  
 [資料流程](../../../integration-services/data-flow/data-flow.md)   
 [Integration Services 轉換](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
