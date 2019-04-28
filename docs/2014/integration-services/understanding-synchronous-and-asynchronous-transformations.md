---
title: 了解同步和非同步轉換 | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- transformations [Integration Services], synchronous and asynchronous
- asynchronous transformations [Integration Services]
- data flow components [Integration Services], synchronous and asynchronous
- synchronous transformations [Integration Services]
ms.assetid: 0bc2bda5-3f8a-49c2-aaf1-01dbe4c3ebba
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8d0ae065c411214a1b86aff29917a34cdcff0e0a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62878058"
---
# <a name="understanding-synchronous-and-asynchronous-transformations"></a>了解同步和非同步轉換
  如需了解 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 之同步與非同步轉換間的差異，可以從了解同步轉換開始著手。 如果同步轉換不符合您的需求，您的設計可能需要非同步轉換。  
  
## <a name="synchronous-transformations"></a>同步轉換  
 同步轉換會處理內送資料列，並在資料流程中傳遞這些資料列 (一次一個資料列)。 輸出會與輸入同步，這表示會同時發生。 因此，若要處理給定的資料列，轉換不需要有關資料集內其他資料列的資訊。 在實際實作中，當資料列從某個元件傳遞給下一個元件時，會分成若干緩衝區，但這些緩衝區對使用者而言是透明的，而且您可以假設每一個資料列都會單獨處理。  
  
 同步轉換的一個範例為資料轉換。 對於每一個內送的資料列而言，它都會轉換指定之資料行中的值，並依照其方式來傳送此資料列。 每一個離散轉換作業都與資料集內的所有其他資料列無關。  
  
 在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]指令碼和程式設計中，您會指定同步轉換查閱元件輸入的識別碼，並將它指派給`SynchronousInputID`元件輸出的屬性。 這樣會告訴資料流程引擎要處理輸入中的每一個資料列，並將每一個資料列自動傳送給指定的輸出。 如果您希望每一個資料列都能進入到每一個輸出，您不需要撰寫任何其他程式碼，也可以輸出資料。 如果您使用 `ExclusionGroup` 屬性來指定資料列應該只能進入到某一組輸出 (如同「條件式分割」轉換中的處理方式)，您必須呼叫 `DirectRow` 方法，才能為每一個資料列選取適當的目的地。 當您有錯誤輸出時，您必須呼叫 `DirectErrorRow`，將有問題的資料列傳送到錯誤輸出，而不是預設輸出。  
  
## <a name="asynchronous-transformations"></a>非同步轉換  
 當您無法將每一個資料列與所有其他資料列分開處理時，您可能會決定您的設計需要非同步處理。 換句話說，當您處理每一個資料列時，您無法在資料流程中傳遞它，但是必須改為以非同步方式輸出資料，或是讓輸出與輸入的時間不同。 例如，下列案例需要非同步轉換：  
  
-   此元件必須取得多個資料緩衝區，然後才可以執行其處理作業。 排序轉換就是一個範例，其中的元件必須在單一作業中處理完整的資料列集。  
  
-   此元件必須結合多個輸入中的資料列。 合併轉換就是一個範例，其中的元件必須檢查每一個輸入中的多個資料列，然後以排序次序來合併它們。  
  
-   輸入資料列和輸出資料列之間有一對一的關係。 彙總轉換就是一個範例，其中的元件必須在輸出中加入資料列，才能保留計算的彙總值。  
  
 在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 指令碼和程式設計中，您會指定非同步轉換，其方式是將 0 的值指派給元件輸出的 `SynchronousInputID` 屬性。 . 這樣會告訴資料流程引擎不要將每一個資料列自動傳送給輸出。 然後您必須撰寫程式碼，明確地將每一個資料列傳送給適當的輸出，其方式是將其加入到針對非同步轉換輸出所建立的新輸出緩衝區內。  
  
> [!NOTE]  
>  由於來源元件也必須明確地將它從資料來源讀取的每一個資料列加入到它的輸出緩衝區內，所以來源類似於具有非同步輸出的轉換。  
  
 此外，也可以建立非同步轉換，使其模擬同步轉換 (其方式是明確地將每一個輸入資料列複製到輸出)。 您可以透過這個方法來重新命名資料行，或是轉換資料類型或格式。 不過，這個方法會降低效能。 您可以達到相同的結果而且有更好的效能，其方式是使用內建 Integration Services 元件，例如複製資料行或資料轉換。  
  
![Integration Services 圖示 （小）](media/dts-16.gif "Integration Services 圖示 （小）")**保持最多包含 Integration Services 的日期**<br /> 若要取得 Microsoft 的最新下載、文件、範例和影片以及社群中的精選解決方案，請瀏覽 MSDN 上的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 頁面：<br /><br /> [瀏覽 MSDN 上的 Integration Services 頁面](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要得到這些更新的自動通知，請訂閱該頁面上所提供的 RSS 摘要。  
  
## <a name="see-also"></a>另請參閱  
 [使用指令碼元件建立同步轉換](data-flow/transformations/script-component.md)   
 [使用指令碼元件建立非同步轉換](extending-packages-scripting-data-flow-script-component-types/creating-an-asynchronous-transformation-with-the-script-component.md)   
 [開發具有同步輸出的自訂轉換元件](extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-synchronous-outputs.md)   
 [開發具有非同步輸出的自訂轉換元件](extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-asynchronous-outputs.md)  
  
  
