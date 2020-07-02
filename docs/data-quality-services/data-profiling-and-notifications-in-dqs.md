---
title: DQS 中的資料分析與通知
ms.date: 04/01/2020
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: a778bb5b-8e35-4a7b-b04a-ae2b46dec21b
author: swinarko
ms.author: sawinark
ms.openlocfilehash: ab254c9deaee5a9e31a89d2a44d281e83a2beead
ms.sourcegitcommit: 6be9a0ff0717f412ece7f8ede07ef01f66ea2061
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85812551"
---
# <a name="data-profiling-and-notifications-in-dqs"></a>DQS 中的資料分析與通知

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 中的資料分析程序會分析現有資料來源中的資料，以及顯示有關 DQS 活動資料的統計資料。 此程序為您提供資料品質的自動化度量。 DQS 分析會整合到 DQS 知識管理與資料品質專案中。 它是動態且可調整的。 分析有兩個主要目標：首先是在資料品質程序中引導您並支援您的決策，第二個目標是評估程序的效用。 DQS 分析程序的優點如下：  
  
-   分析會提供來源資料品質的洞察能力，並幫助您識別資料品質問題。  
  
-   分析會評估資料品質程序的效用，引導您進行知識探索、資料清理、比對原則和比對工作。  
  
-   分析為您呈現最相關之時間的最相關資訊。  
  
-   分析程式會產生通知，以強調可能採取行動的重要統計資料或事件。 在許多情況下，DQS 通知將會指示情況，並建議補救該狀況所可以採取的動作。  
  
 分析讓您不僅將 Data Quality Services 用於知識探索、清理和比對，也可以當做分析工具。 您可能會想要建立一個知識庫進行分析，並使用該知識庫執行知識探索，根據分析統計資料判斷此知識庫是否滿足您的探索、清理和比對需求。  
  
##  <a name="how-profiling-works"></a><a name="How"></a> 分析的運作方式  
 分析不會測量知識庫的品質。 而會衡量來源資料的品質。 分析會提供統計資料，指出您在知識管理或來源資料的資料品質專案中執行之特定作業的效果。 分析一定會在您所執行之特定活動的內容中。 您可以按一下畫面中的 [分析] 索引標籤，以顯示程式碼剖析資料，而不需要離開您所執行之活動的階段。 執行程式時，分析資料表會即時填入，讓您能夠在執行資料品質工作時進行評估。 您可以在清理或刪除重複作業之後判斷來源資料是否變得比較好以及變好的程度。  
  
 所有分析編號都會參考值的外觀數目，而在許多情況下，會參考總計的百分比，但唯一性計量除外。 唯一性度量會參考值的絕對數目，不論這些值出現多少次。  
  
 分析是 DQS 知識驅動之方案的一部分。 它會根據資料來源欄位與知識庫定義域之間的對應，提供有關知識庫、比對或資料清理程序的資訊。 您只會在對應完成後進行分析;任何活動的對應階段期間都不會進行任何分析。 分析一定會附加至活動。 分析的程式是針對對應至定義域的資料進行，而不是在定義域中的資料上進行。 它會整合到下列活動步驟中：  
  
-   知識探索活動的 **[探索]** 和 **[管理定義域值]** 步驟  
  
-   清理活動的 **[清理]** 和 **[管理和檢視結果]** 步驟  
  
-   比對原則活動的 **[比對原則]** 和 **[比對結果]** 步驟  
  
-   比對活動的 **[比對]** 和 **[匯出]** 步驟  
  
 DQS 不會提供定義域管理活動的分析統計資料。  
  
##  <a name="profiling-data-by-activity"></a><a name="Activity"></a> 依據活動分析資料  
 DQS 分析會使用標準資料品質維度來表示資料的品質：完整性 (資料存在的程度) 和精確度 (可將資料用於預定用途的程度)，以及唯一性 (不同值代表不同實體的程度)。 根據預設，Null 和空白值會被視為遺漏，或降低完整性百分比;不過，您也可以將其他值定義為 Null 對等，在這種情況下，它們也會被視為遺漏。  
  
 分析為您提供評估程序所需的統計資料，但是您必須解譯這些統計資料。 請按資料行逐一查看這些統計資料，以理解分析要告訴您什麼事。  
  
 DQS 活動具有不同的分析統計資料集合，如下所示：  
  
-   只有清理活動才擁有精確度分析統計資料 (依定義域以百分比表示)。 精確度會受到有效性、一致性、語法錯誤和定義域規則的影響。  
  
-   只有清理活動才擁有來源中之正確、已更正和建議的分析統計資料，以及依定義域的更正和建議值 (兩個數字都是以百分比表示)。  
  
-   清理和知識探索活動具有有效性的分析統計資料 (依記錄的清理，以及依記錄和定義域的知識探索)。 比對原則和比對活動沒有有效性的統計資料。  
  
-   清理活動沒有唯一性的分析統計資料。 知識探索、比對原則和比對活動具有唯一性的分析統計資料 (針對來源以及依定義域以數字和百分比表示)。  
  
 如需與活動相關之特定分析統計資料的詳細資訊，請參閱下列文章中的分析章節：  
  
-   [執行知識探索](../data-quality-services/perform-knowledge-discovery.md)  
  
-   [使用 DQS &#40;內部&#41; 知識清理資料](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md)  
  
-   [建立比對原則](../data-quality-services/create-a-matching-policy.md)  
  
-   [執行比對專案](../data-quality-services/run-a-matching-project.md)  
  
##  <a name="profiling-data-in-activity-monitoring"></a><a name="Monitoring"></a>活動監控中的分析資料  
 知識探索、比對原則、比對和清理活動的分析資訊，不僅適用于 Data Quality client 中的活動頁面，還可在活動監視中使用。 活動監控為您提供目前和過去活動的概觀。 除了活動的屬性及相關的計算程序之外，您也可以檢視針對某個位置的每一個活動所產生的分析資訊。 您可在活動資料表中選取活動，於底下的資料表中顯示分析結果。 您也可以匯出分析結果。 如需詳細資訊，請參閱 [DQS Administration](../data-quality-services/dqs-administration.md)。  
  
##  <a name="notifications"></a><a name="Notifications"></a> 通知  
 除了透過分析來收集及顯示重要統計資料與度量以外，DQS 也會產生通知 (如果啟用的話)，以指示您何時可能會想要根據顯示的分析統計資料來採取動作。 DQS 會使用通知來強調有關資料來源的重要事實，以及顯示目前活動與其執行目的相較之下的效果。 通知所提供的提示與建議會指示情況，並建議您如何改善知識探索、資料清理或資料比對活動。  
  
 DQS 通知是用來引發您可能會感興趣的問題，或是對付潛在問題。 您是否根據通知採取動作，取決於其是否與您的用途有關。 例如，假設 DQS 在以下情況下發佈通知：資料清理未產生任何更正值或建議值，而完整性與精確度同時為 100%。 此通知指示，該活動可能不需要執行。 但是，不論您是否選擇執行活動，都是您自己的決定。  
  
 通知是由工具提示以 [**分析**] 索引標籤中的驚嘆號表示。與通知相關聯的統計資料會以紅色顯示，表示通知的統計理由。  
  
 您可以在 Data Quality Client 首頁之 **[管理]** 區段的 **[一般設定]** 索引標籤中，啟用 (預設值) 或停用通知。 當停用通知時，不會顯示工具提示，而且統計資料不會以紅色著色。 停用通知並不會大幅改善效能。 如果您停用通知，分析依然可運作。  
  
 如需與活動通知相關聯的特定條件，請參閱下列文章：  
  
-   [執行知識探索](../data-quality-services/perform-knowledge-discovery.md)  
  
-   [使用 DQS &#40;內部&#41; 知識清理資料](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md)  
  
-   [建立比對原則](../data-quality-services/create-a-matching-policy.md)  
  
-   [執行比對專案](../data-quality-services/run-a-matching-project.md)  
  
## <a name="related-tasks"></a>相關工作  
  
|工作描述|發行項|  
|----------------------|-----------|  
|描述如何啟用或停用 DQS 中的通知。|[在 DQS 中啟用或停用分析通知](../data-quality-services/enable-or-disable-profiling-notifications-in-dqs.md)|  
  
  
