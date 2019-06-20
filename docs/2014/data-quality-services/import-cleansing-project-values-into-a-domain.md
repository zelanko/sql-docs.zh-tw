---
title: 將清理專案值匯入定義域 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql12.dqs.kb.importprojectvalues.f1
ms.assetid: f23e38e2-39e0-42d7-abd5-34d8fcca5d2a
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: c5661d490f4669968b6d8198a7565fb5e5c8c218
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65484300"
---
# <a name="import-cleansing-project-values-into-a-domain"></a>將清理專案值匯入定義域中
  在 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 中，您可以將清理程序期間，於資料品質清理專案或 Integration Services 封裝 (包含 DQS 清理元件) 中所收集的資料品質知識，匯入定義域中。 如此可確保可靠的知識不會遺失，而且會持續改良知識庫。  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Prerequisites"></a> 必要條件  
  
-   若要將清理專案值匯入定義域，您必須已經在 Data Quality Client 或 Integration Services 封裝 (包含 DQS 清理元件) 的清理專案中使用該定義域。  
  
-   您必須已經順利執行完 Data Quality Client 或 Integration Services 封裝 (包含 DQS 清理元件) 中的清理專案。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
 您必須擁有 DQS_MAIN 資料庫的 dqs_kb_editor 角色或 dqs_administrator 角色，才能將清理程序期間所收集的資料品質知識匯入定義域中。  
  
##  <a name="Import"></a> 匯入清理專案值  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [執行 Data Quality Client 應用程式](../../2014/data-quality-services/run-the-data-quality-client-application.md)。  
  
2.  在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 首頁畫面中，於 [定義域管理] 活動中開啟知識庫。  
  
3.  如果您要將值加入至現有的定義域，請在定義域清單中選取定義域。  
  
4.  按一下 **[定義域值]** 索引標籤、按一下圖示列中的 **[匯入值]** 圖示，然後按一下 **[匯入專案值]** 。 **[匯入專案值]** 對話方塊隨即顯示，並提供使用定義域進行清理之資料品質專案和 Integration Services 封裝的清單。  
  
    > [!NOTE]  
    >  如果尚未使用定義域或是其連結的任何定義域建立任何專案，或者專案尚未完成，將無法使用 **[匯入專案值]** 選項。  
  
5.  在 **[匯入專案值]** 對話方塊中：  
  
    -   在 **[已匯入]** 下拉式清單中，選取 **[全部]** 顯示所有專案，或選取 **[否]** 只顯示尚未匯入值的專案。  
  
    -   選取要匯入的值來自於哪一個專案。  
  
    -   選取 **[加入 [新增] 索引標籤中的值]** ，除了 **[正確]** 和 **[更正]** 索引標籤中的值以外，也匯入 [新增] 索引標籤中的值。  
  
    -   按一下 [確定]  。  
  
6.  當您返回 **[定義域值]** 索引標籤之後，成功匯入值的訊息隨即顯示。 已經匯入所以對定義域而言為新增的值將會顯示在 **[值]** 資料表中。  
  
7.  取消選取 **[只顯示新值]** ，顯示定義域中的所有值。  
  
8.  選取 **[正確]** 、 **[錯誤]** 或 **[無效]** ，只顯示所選類型的值。  
  
9. 若要搜尋特定字串，請在 **[尋找]** 文字方塊中輸入此字串。 按一下向上或向下箭號，逐步瀏覽符合搜尋準則的值。 這些值將會以黃色反白顯示。  
  
10. 按一下 **[完成]** 。  
  
    > [!NOTE]  
    >  如需有關使用 **[定義域值]** 索引標籤中之值的詳細資訊，請參閱＜ [Change Domain Values](../../2014/data-quality-services/change-domain-values.md)＞。  
  
##  <a name="FollowUp"></a> 後續操作：將專案值匯入定義域之後  
 在您將清理程序期間所收集的資料品質知識匯入定義域之後，您可以針對定義域和值執行其他定義域管理工作。 如需詳細資訊，請參閱[管理定義域](../../2014/data-quality-services/managing-a-domain.md)。  
  
##  <a name="Values"></a> 將會匯入的值  
 以下的值將會從專案匯入定義域中：  
  
-   只有字串值會匯入定義域。  
  
-   只會匯入 **[清理]** 活動的 **[管理和檢視結果]** 頁面上，位於 **[正確]** 、 **[更正]** 和 **[新增]** 索引標籤中的值。 **[新增]** 索引標籤中的值只有已在 **[匯入專案值]** 對話方塊中選取 **[加入 [新增] 索引標籤中的值]** 核取方塊時才會匯入。  
  
-   值將會以正確值或是包含更正的錯誤形式匯入。 只會匯入包含更正值的錯誤值。  
  
-   更正值將會是不存在於知識庫中的新值，或是現有的正確值。  
  
-   只有在值層級而不是記錄層級執行的更正才會匯入知識庫中。  
  
-   如果匯入的值與定義域規則衝突，將會建立無效的值。  
  
-   如果您一次匯入幾個專案中的值，則會循序匯入這些值。  
  
-   定義域中以詞彙為主的關聯所產生的更正將會當做正確值 (而不是錯誤) 匯入。  
  
##  <a name="ValuesNot"></a> 將不會匯入的值  
 以下的值將不會從專案匯入定義域中：  
  
-   **[清理]** 活動的 **[管理和檢視結果]** 頁面上 **[建議]** 和 **[無效]** 索引標籤中的值將不會匯入。  
  
-   如果清理專案中找到的值與定義域中的現有值衝突，則會略過專案中找到的值。 這包括清理值與知識庫值之間的衝突。  
  
-   在記錄層級執行的更正將不會匯入知識庫中。  
  
-   如果將取代的值已更正或是由參考資料服務核准為正確，則不會將任何值匯入定義域中。  
  
-   如果更正值以無效或錯誤值的形式出現在知識庫中，則錯誤和更正值都不會匯入。  
  
-   如果定義域是複合定義域的一部分，而且已針對複合定義域執行清理，則不會匯入任何值。  
  
-   只有當知識庫的狀態為工作中，而且知識庫由正在匯入的使用者鎖定時，您才可以從專案匯入值。  
  
## <a name="see-also"></a>另請參閱  
 [資料清理](../../2014/data-quality-services/data-cleansing.md)   
 [DQS 清理轉換](../integration-services/data-flow/transformations/dqs-cleansing-transformation.md)  
  
  
