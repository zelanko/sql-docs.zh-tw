---
title: DQS 中的資料分析與通知
ms.date: 03/15/2020
ms.prod: sql
ms.reviewer: jroth
ms.technology: data-quality-services
ms.topic: conceptual
author: swinarko
ms.author: sawinark
ms.openlocfilehash: e0bd9585a48ee30368d145c79f8431e922801a9c
ms.sourcegitcommit: c30a2def43c86860aeec69d3e3029f2296544b13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/25/2020
ms.locfileid: "80243398"
---
# <a name="data-profiling-and-notifications-in-data-quality-services-dqs"></a>Data Quality Services （DQS）中的資料分析和通知

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

[!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)]（DQS）是一種資料分析服務。 DQS 會分析來源中的資料，並顯示 DQS 活動中資料的相關統計資料。

## <a name="attributes-goals-benefits"></a>屬性、目標、優點

### <a name="attributes-of-dqs"></a>DQS 的屬性

DQS 分析具有下列屬性：

- 提供資料品質的自動化測量。
- 已整合到 DQS 知識管理和資料品質專案。
- 是動態且可調整的。

### <a name="goals-of-dqs"></a>DQS 的目標

使用 DQS 進行分析有下列兩個主要目標：

- 引導您完成資料品質處理常式，並支援您的決策。
- 以評估處理常式的有效性。

### <a name="benefits-of-dqs"></a>DQS 的優點

DQS 分析具有下列優點：

- 提供來源資料品質的深入解析，並協助您識別資料品質問題。

- 評估資料品質處理常式，並引導您：
  - 知識探索
  - 資料清理
  - 比對原則
  - 符合工作

- 在最相關的時間提供您最相關的資訊。

- 產生通知，強調可能會有動作的重要統計資料或事件。 DQS 通知通常會指出條件，並建議矯正措施。

DQS 分析會提供知識探索、資料清理和資料比對。 DQS 也是資料分析工具。 您可以建立用於分析的知識庫。 然後，您就可以使用知識庫來執行知識探索。 知識探索會流量分析統計資料來判斷知識庫是否符合您對探索、清理和比對的需求。

## <a name="how-dqs-profiling-works"></a><a name="How"></a>DQS 分析的運作方式

DQS 分析不會測量知識庫的品質。 分析會測量來源資料的品質。 分析提供的統計資料會指出下列工作的影響：

- 知識管理中的特定作業。
- 來源資料上的資料品質專案。

### <a name="activity-context"></a>活動內容

分析一定會在您所執行之特定活動的內容中。 您可以按一下畫面中的 [分析] 索引標籤，以顯示程式碼剖析資料。 這種按一下並不會讓您離開正在執行的活動階段。 執行進程時，會即時填入分析資料表。 因此，您可以在執行資料品質工作時進行評估。

您可以在清理或刪除重複作業之後判斷來源資料是否變得比較好以及變好的程度。

### <a name="profiling-is-based-on-counts"></a>分析是根據計數

所有分析編號都會參考特定值的外觀計數。 在許多情況下，數位會參考總計的百分比。 唯一性計量是例外狀況。 無論這些值的外觀計數為何，唯一性計量都會參考絕對值的絕對數目。

### <a name="knowledge-driven-solution"></a>知識驅動方案

分析是 DQS 知識驅動之方案的一部分。 分析提供知識庫、比對或資料清理程式的相關資訊。 此資訊是以資料來源欄位與知識庫網域之間的對應為基礎。 只有在完成對應之後，才會執行程式碼剖析。 任何活動的對應階段期間都不會執行任何分析。

分析一定會附加至活動。 分析程式是針對_對應_至定義域的資料執行，而不是在定義域_中_的資料上執行。

分析會整合到以下的活動步驟中：

- 知識探索活動的 [**探索**] 和 [**管理定義域值**] 步驟。

- 清理活動的**清理**和**管理和查看結果**步驟。

- 符合原則活動的比對**原則**和比對**結果**步驟。

- 相符**活動的比對和****匯出**步驟。

DQS 不會提供 [定義域管理] 活動的分析統計資料。

## <a name="profiling-data-by-activity"></a><a name="Activity"></a>依據活動分析資料

DQS 分析會使用下列標準資料品質維度來表示資料的品質：

- 完整性-資料的存在程度。
- 精確度-資料可用於其預定用途的範圍。
- 唯一性-不同值代表不同實體的範圍。

根據預設，Null 和空白值會被視為遺漏，或降低完整性百分比。 不過，您可以將其他值定義為 Null 對等。 這些值也會被視為遺漏。

分析為您提供評估程序所需的統計資料，但是您必須解譯這些統計資料。 請按資料行逐一查看這些統計資料，以理解分析要告訴您什麼事。

### <a name="differing-sets-of-profiling-statistics"></a>不同組的分析統計資料

DQS 活動具有不同的分析統計資料集合，如下所示：

- 只有清理活動才擁有精確度分析統計資料 (依定義域以百分比表示)。 精確度會受到有效性、一致性、語法錯誤和定義域規則的影響。

- 只有清理活動才擁有來源中之正確、已更正和建議的分析統計資料，以及依定義域的更正和建議值 (兩個數字都是以百分比表示)。

- 清理和知識探索活動具有有效性的分析統計資料 (依記錄的清理，以及依記錄和定義域的知識探索)。 比對原則和比對活動沒有有效性的統計資料。

- 系統會針對來源和網域提供唯一性的分析統計資料。 此語句適用于下列活動：
  - 知識探索。
  - 比對原則。
  - 找到.
  - 但_不適_用於清理活動。

DQS 提供與活動相關的特定分析統計資料。 如需詳細資訊，請參閱下列主題中的**分析**章節：

- [執行知識探索](../data-quality-services/perform-knowledge-discovery.md)

- [使用 DQS &#40;內部&#41; 知識清理資料](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md)

- [建立比對原則](../data-quality-services/create-a-matching-policy.md)

- [執行比對專案](../data-quality-services/run-a-matching-project.md)

## <a name="profiling-data-in-activity-monitoring"></a><a name="Monitoring"></a>活動監控中的分析資料

分析資訊不僅適用于 Data Quality client 的活動頁面，也可以在活動監視中使用。 這些資訊會關心知識探索、比對原則、比對和清理活動。 此資訊可在資料品質用戶端的 [活動] 頁面和 [活動監控] 中取得。

您可以在一個位置中查看下列所有專案：

- 屬性
- 活動的相關計算處理常式
- 針對每個活動產生的程式碼剖析資訊

您可以在 [活動] 資料表中選取活動，以在第二個數據表中顯示分析結果。 您也可以匯出分析結果。

如需詳細資訊，請參閱 [DQS Administration](../data-quality-services/dqs-administration.md)。

## <a name="notifications"></a><a name="Notifications"></a>提醒

DQS 會產生通知，指出您可能想要根據分析的統計資料採取動作。 DQS 會使用通知來取得有關資料來源的重要事實。 這些事實會顯示目前活動相對於其執行目的的效果。 通知會提供指示條件的秘訣和建議。 通知也可能會建議您如何改善知識探索、資料清理或資料比對活動。

DQS 會在偵測到您可能對您很重要的問題時傳送通知。 舉例來說，當完整性和精確度兩者都是100% 時，資料清理活動可能不會產生更正或建議的值。 DQS 可能會在這種情況下張貼通知。 此通知會指出可能不需要活動。 是否執行活動仍然是您的決定。

在 [**分析**] 索引標籤中，具有驚嘆號的工具提示會指出通知。與通知相關聯的統計資料會以紅色顯示，表示通知的統計理由。

### <a name="disable-notifications"></a>停用通知

預設會啟用通知。 但您可以使用 [Data Quality Client] 首頁來停用通知。 在 [系統**管理**] 區段中，使用 [**一般設定**] 索引標籤。

當停用通知時，不會顯示工具提示，而且統計資料也不會以紅色著色。 停用通知時，分析仍然可以運作。 停用通知並不會改善效能。

如果是與活動之通知有關的特定情況，請參閱下列資源：

- [執行知識探索](../data-quality-services/perform-knowledge-discovery.md)

- [使用 DQS &#40;內部&#41; 知識清理資料](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md)

- [建立比對原則](../data-quality-services/create-a-matching-policy.md)

- [執行比對專案](../data-quality-services/run-a-matching-project.md)

## <a name="related-tasks"></a>相關工作

| 工作描述 | 主題 |
| :--------------- | :---- |
| 描述如何啟用或停用 DQS 中的通知。 | [在 DQS 中啟用或停用分析通知](../data-quality-services/enable-or-disable-profiling-notifications-in-dqs.md) |
|||
