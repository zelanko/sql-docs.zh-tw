---
title: 快取重新整理選項 （報表管理員） |Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 227da40c-6bd2-48ec-aa9c-50ce6c1ca3a6
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 05f2cdfc40c8677bfa38c821cfd849c3ce483c31
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/22/2019
ms.locfileid: "59964194"
---
# <a name="cache-refresh-options-report-manager"></a>快取重新整理選項 (報表管理員)
  使用 [快取重新整理] 選項頁面來建立排程，以供預先載入含報表或共用資料集資料暫存副本的快取。 重新整理計劃包括排程和選項，可指定或覆寫參數的值。 您不能針對共用資料集，覆寫標示為唯讀的參數值。 您可以建立並使用多個重新整理計劃做為重新整理選項頁面的一部分。  
  
 可讓您加入、刪除、變更及檢視快取重新整理計劃之相關報表和共用資料集的預設角色指派有：[內容管理員]、[我的報表] 和 [發行者]。  
  
> [!NOTE]  
>  並非所有 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]版本都提供此功能。 如需的版本所支援的功能清單[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，請參閱 <<c2> [ 支援的 SQL Server 2014 的版本功能](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)。  
  
## <a name="to-open-the-cache-refresh-plan-properties-page-for-a-report-or-shared-dataset"></a>開啟報表或共用資料集的快取重新整理計劃屬性頁  
  
1.  開啟報表管理員，然後找出您想要設定快取重新整理計劃屬性的報表或共用資料集。  
  
2.  將滑鼠停留在報表或共用資料集上方，然後按下拉式箭號。  
  
3.  在下拉式清單中，按一下 **[管理]**， **[一般屬性]** 頁面隨即開啟。  
  
4.  按一下 **[快取重新整理計劃]** 索引標籤。  
  
5.  若要建立新的快取計劃，請按一下 **[新增快取重新整理計劃]**。  
  
    > [!NOTE]  
    >  您必須啟用並啟動 SQL Server Agent 服務來建立快取重新整理計劃。  
  
6.  若要建立一份快取計劃，然後加以自訂，請按一下 **[從現有的新增]**。  
  
## <a name="cache-refresh-options"></a>快取重新整理選項  
 **刪除**  
 刪除目前選取的所有重新整理計劃。  
  
 **從現有的新增**  
 當只選取一個快取重新整理計劃時，會啟用此選項。 這個選項會建立從原始計劃複製的新重新整理計劃。 [快取重新整理計劃] 頁面開啟時會預先填入所選取計劃的詳細資料。 接著，您就可以修改重新整理計劃選項，然後使用新的描述儲存該計劃。  
  
 **新的快取重新整理計劃**  
 按一下可建立新的重新整理計劃，以用於目前的快取重新整理選項中。  
  
 **編輯**  
 選取這個選項，以編輯目前的重新整理計劃。  
  
## <a name="cache-refresh-plan-options"></a>快取重新整理計劃選項  
 **說明**  
 指定快取重新整理計劃的描述。  
  
 **項目特定排程**  
 選取此選項，可建立僅供此項目使用的排程。  
  
 **設定**  
 按一下即可開啟 [排程] 頁面，可用來指定頻率資訊。  
  
 如需詳細資訊，請參閱[新的排程：編輯排程頁面&#40;報表管理員&#41;](../../2014/reporting-services/new-schedule-edit-schedule-page-report-manager.md)。  
  
 **共用的排程**  
 選取此選項，可選取現有的排程。  
  
 如需詳細資訊，請參閱 [Create, Modify, and Delete Schedules](subscriptions/create-modify-and-delete-schedules.md)。  
  
 **@\<** *參數* **>**  
 指定參數值的其中一個組合。 此區段只有在目前的資料集或報表具有參數時才會出現。  
  
 請參閱下一節中的 [指定參數](#Parameters) 。  
  
 **使用預設值**  
 選取此選項，可使用此參數的預先定義預設值。  
  
##  <a name="Parameters"></a> 指定參數  
 若要建立快取重新整理計劃，每個報表或共用資料集參數都必須有值。 如果報表或共用資料集項目並沒有在定義中指定預設值，您必須指定一個值。 如果有預設值，就不需要在此提供值。 如果您提供了任何值，該值就會覆寫預設值。  
  
 若要指定多個參數值組合，請分別為每個值組合建立快取重新整理計劃。  
  
 對報表或共用資料集上的參數進行新增、變更及刪除都可能會影響快取重新整理計劃。 如果您加入含報表預設值的參數、移除參數，或變更共用資料集參數的資料類型或唯讀選項，變更會在下一次處理快取重新整理計劃時生效。  
  
### <a name="shared-dataset-parameters"></a>共用資料集參數  
 就共用資料集而言，下列資訊是自共用資料集定義衍生而來：  
  
-   **名稱** ：指定查詢參數的名稱。  
  
-   **類型** ：指定查詢參數的資料類型。 由於直到資料提供者處理資料集查詢之前，資料類型都屬未知，所以處理共用資料集之前無法進行資料類型驗證。  
  
-   **可為 Null** ：指定 NULL 是否為有效的值。  
  
-   **唯讀** ：指定這個參數在共用資料集定義中是否標示為唯讀。 唯讀參數不會顯示在快取重新整理選項的參數清單中，而且必須指定預設值做為共用資料集定義的一部分。  
  
-   **預設值** ：已在共用資料集定義中指定的預設值。 查詢參數可以是多重值。 若要覆寫預設值，請在文字方塊提示區域中輸入新的值。  
  
 如果共用資料集定義為參數指定 **[從查詢中忽略]** 選項，就不需要提供預設值。 這個旗標表示查詢中不使用該資料集參數。 例如，參數顯示在共用資料集定義中，因為該參數是只用於資料集篩選中的報表參數。  
  
 若要檢視或變更資料集參數選項，您必須編輯共用資料集定義。 如需詳細資訊，請參閱 [Manage Shared Datasets](report-data/manage-shared-datasets.md)(管理共用資料集)。  
  
### <a name="report-parameters"></a>報表參數  
 依報表來說，每個參數值都必須有效，才能順利建立快取重新整理計劃。 您必須為每個報表參數輸入或選取預設值。 您所設定的值會覆寫在報表伺服器上為報表參數定義的預設值。  
  
 參數必須符合報表伺服器上參數屬性中指定的需求。 比方說，如果屬性 AllowBlank 是為報表參數，則為 false，空字串不是有效的值。  
  
 若要檢視或變更報表參數選項，必須在報表中編輯報表參數，或是另外在報表伺服器上獨立編輯。 如需詳細資訊，請參閱 <<c0> [ 報表參數概念&#40;報表產生器及 SSRS&#41;](report-design/report-parameters-concepts-report-builder-and-ssrs.md)。</c0>  
  
## <a name="conditions-that-cause-a-cache-refresh-plan-to-be-inactive"></a>導致快取重新整理計劃成為非使用狀態的條件  
 下列條件可能會導致共用資料集或報表快取重新整理計畫變成非使用狀態。  
  
-   共用資料集快取或報表快取選項會停用。  
  
-   必要的參數值為未定義、無效或遺漏。 報表的所有查詢都必須有效，報表才會進行處理。 對於具有子報表的報表，會先處理所有資料集查詢 (包括子報表的資料集在內)。 如果無法順利處理任何資料集，報表就無法執行。  
  
## <a name="conditions-that-cause-a-cache-refresh-plan-to-be-reactivated"></a>使得快取重新整理計劃重新啟動的條件  
 計劃處於非使用狀態後，請執行下列其中一項以觸發快取重新整理計劃的評估程序：  
  
-   變更計劃的選項。  
  
-   啟用與重新整理計劃相關聯的共用資料集或報表快取。  
  
-   為與重新整理計劃關聯的資料集查詢參數清除或選取唯讀選項，然後將新的定義儲存至報表伺服器。  
  
## <a name="see-also"></a>另請參閱  
 [項目層級工作](security/tasks-and-permissions-item-level-tasks.md)   
 [報表管理員 &#40;SSRS 原生模式&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [報表管理員 F1 說明](../../2014/reporting-services/report-manager-f1-help.md)   
 [快取多個報表 &#40;SSRS&#41;](report-server/caching-reports-ssrs.md)   
 [管理共用資料集](report-data/manage-shared-datasets.md)  
  
  
