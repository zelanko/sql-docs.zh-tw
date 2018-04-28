---
title: 建立以詞彙為主的關聯 | Microsoft Docs
ms.custom: ''
ms.date: 11/08/2011
ms.prod: sql
ms.prod_service: data-quality-services
ms.service: ''
ms.component: data-quality-services
ms.reviewer: ''
ms.suite: sql
ms.technology:
- data-quality-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.dqs.dm.kbtermsbased.f1
ms.assetid: 66db9277-d892-4dae-8a82-060fd3ba6949
caps.latest.revision: 27
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 74ee51eca04f98d819854116342514b3980bd1b9
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="create-term-based-relations"></a>建立以詞彙為主的關聯

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  此主題描述如何針對 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 中的定義域建立以詞彙為主的關聯。 以詞彙為主的關聯 (TBR) 可讓您針對屬於定義域值的詞彙進行更正。 它會啟用多個值，這些值除了被視為相同同義字的共同部分拼字以外，都是相同的。 例如，您可以設定某個以詞彙為主的關聯，將 “Inc.” 詞彙變更為 “Incorporated”。 每當在定義域中遇到 “Inc.” 詞彙時，都會加以變更。 出現 “Contoso, Inc.” 的地方將會變更為 “Contoso, Incorporated”，而且這兩個值會被視為完全相符的同義字。  
  
 若要使用以詞彙為主的關聯，請建立「值/更正為」配對清單，例如 “Inc.” 和 “Incorporated” 或是 “Senior” 和 “Sr.”。 使用以詞彙為主的關聯可讓您在整個定義域中變更詞彙，而不需要手動將個別定義域值設定為同義字。 您可以指定應該更正某個值，即使知識探索之前尚未探索該值。 如果以詞彙為主的關聯轉換讓兩個值變成完全相同，則 DQS 將會在兩者之間建立同義字關聯性 (在知識探索中)、在兩者之間建立更正關聯性 (在資料更正中)，或是建立完全相符的項目 (在比對中)。  
  
 在分析之前，以詞彙為主的關聯轉換和符號轉換 (其中會以空格或 null 取代特殊字元) 都會在前置處理階段進行。 如果要求複合定義域剖析，則會在兩次轉換之前執行，因為分隔符號剖析需要符號。 其他作業 (例如定義域規則和定義域值變更) 將會在轉換之後執行。 就比對而言，不論您是否執行了清理，都會在比對活動之前，將以詞彙為主的關聯套用至來源資料。  
  
 **以詞彙為主的關聯及定義域管理**  
  
 當您在定義域管理中套用以詞彙為主的關聯時，DQS 會在知識探索、清理或比對程序中套用變更，但是 DQS 不會變更定義域值本身以符合以詞彙為主的關聯。 換句話說，如果您在 **[定義域管理]** 頁面的 **[以詞彙為主的關聯]** 索引標籤中，輸入並接受以詞彙為主的關聯，就不會對相同頁面的 **[定義域值]** 索引標籤進行變更。 這可讓您隨後變更 TBR。  
  
 **以詞彙為主的關聯及資料清除**  
  
 當您在定義域中套用以詞彙為主的關聯，並接著執行資料清理程序時，DQS 會在清理期間套用變更，但是不會將變更套用至知識庫中的詞彙。  
  
-   如果依照定義域中以詞彙為主的關聯變更之值不是同義字，該值會顯示在 **[管理和檢視結果]** 頁面之 **[更正]** 索引標籤底下的 **[更正為]** 欄中，且 [原因] 會設定為 [以詞彙為主的關聯]。  
  
-   如果依照以詞彙為主的關聯變更之值不在定義域中，且 DQS 找到相符的值，則會更正為此值，並根據信賴等級出現在 [更正] 索引標籤或 [建議] 索引標籤底下。 如果找不到相符項目，該值會出現在 [新增] 底下，並提供 TBR 更正。 進行此作業的原因是即使您更正 TBR，並不表示該值正確。  
  
-   如果依照以詞彙為主的關聯變更之值在定義域中，但是該值錯誤/無效且存在更正，則該值會出現在 [更正] 索引標籤底下，並提供其更正和原因 ([定義域值])。  
  
-   如果依照以詞彙為主的關聯變更之值在定義域中，但是該值錯誤/無效且無更正，則該值會出現在 [無效] 索引標籤底下，並提供原因 ([定義域值])。  
  
 **以詞彙為主的關聯及知識探索**  
  
 當您套用以詞彙為主的關聯，並接著執行知識庫探索程序時，所有符合 TBR 的值都會維持不變，並會視為正確值。 TBR 變更的任何值會當做正確值匯入，並視為符合 TBR 之值的同義字。  
  
 **以詞彙為主的關聯及將清理值匯入定義域中**  
  
 如果您將清理程序期間收集到的資料品質知識匯入定義域，TBR 變更的值會當做正確值匯入。  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Prerequisites"></a> 必要條件  
 若要建立以詞彙為主的關聯，您必須已在 [定義域管理] 活動中開啟定義域。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
 您必須擁有 DQS_MAIN 資料庫的 dqs_kb_editor 角色或 dqs_administrator 角色，才能建立以詞彙為主的關聯。  
  
##  <a name="Create"></a> 建立以詞彙為主的關聯  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [執行 Data Quality Client 應用程式](../data-quality-services/run-the-data-quality-client-application.md)。  
  
2.  在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 首頁畫面上，開啟或建立知識庫。 選取 **[定義域管理]** 當做活動，然後按一下 **[開啟]** 或 **[建立]**。 如需相關資訊，請參閱 [建立知識庫](../data-quality-services/create-a-knowledge-base.md) 或 [開啟知識庫](../data-quality-services/open-a-knowledge-base.md)。  
  
    > [!NOTE]  
    >  定義域管理會在 Data Quality Services 用戶端的頁面上執行，該頁面包含個別定義域管理作業所適用的五個索引標籤。 這不是精靈驅動的程序，任何管理作業都可以個別執行。  
  
3.  從 **[定義域管理]** 頁面的 **[定義域清單]** 中，選取您想要建立定義域規則的定義域，或是建立新的定義域。 如果您必須建立新的定義域，請參閱＜ [建立定義域](../data-quality-services/create-a-domain.md)＞。  
  
4.  按一下 **[以詞彙為主的關聯]** 索引標籤。  
  
5.  依照以下方式建立以詞彙為主的關聯：  
  
    1.  按一下 **[加入新關聯]** ，將資料列加入至關聯資料表。  
  
    2.  在加入之資料列的 **[值]** 資料行中，輸入詞彙，每當選定定義域內的值出現此詞彙時，您會想要加以變更。  
  
        > [!NOTE]  
        >  如果此詞彙在定義域中是以整個值的形式存在，或者此詞彙在定義域中已經以更正值的形式存在，您會得到錯誤。  
  
    3.  在 **[更正為]** 資料行中輸入詞彙，這是您在 **[值]** 資料行中想要變更成為的詞彙。  
  
    4.  再次按一下 **[加入新關聯]** ，加入另一個以詞彙為主的關聯。  
  
    5.  按一下 **[刪除選取的關聯]** ，從關聯資料表中刪除一個或多個選取的資料列。 您可以按 Ctrl 按鈕然後按一下未選取的資料列，以選取多個資料列。  
  
    6.  在 **[尋找]** 文字方塊中輸入一個或多個位數，以尋找關聯資料表中的值。 系統會反白顯示此字串的相符項目。 使用上下箭頭，移到此字串在資料表中的不同出現位置。  
  
    7.  **拼字檢查**：如果 **[值]** 或 **[更正為]** 資料行中的某個值有波浪式紅色底線，則表示拼字檢查建議此值的更正。 以滑鼠右鍵按一下加上底線的值，並且選取拼字檢查建議的其中一個值。 或者，您可以按一下快速鍵功能表中的 **[加入]** ，繼續使用原始值。 如需相關資訊，請參閱 [使用 DQS 拼字檢查](../data-quality-services/use-the-dqs-speller.md) 及 [設置域屬性](../data-quality-services/set-domain-properties.md)。  
  
        > [!NOTE]  
        >  若要使用拼字檢查，您可以在 **[定義域屬性]** 頁面中啟用此功能，或者如果 **[定義域屬性]** 頁面中已停用此功能，您可以按一下 **[以詞彙為主的關聯]** 頁面上的 **[啟用/停用拼字檢查]** 圖示，在此頁面上啟用此功能。  
  
6.  按一下 **[套用變更]** ，將以詞彙為主的關聯套用至定義域。  
  
7.  按一下 **[完成]** ，完成定義域管理活動，如＜ [End the Domain Management Activity](http://msdn.microsoft.com/library/ab6505ad-3090-453b-bb01-58435e7fa7c0)＞中所述。  
  
##  <a name="FollowUp"></a> 後續操作：建立以詞彙為主的關聯之後  
 在您建立以詞彙為主的關聯之後，您可以針對定義域執行其他定義域管理工作、執行知識探索來將知識加入至定義域，或者將比對原則加入至定義域。 如需詳細資訊，請參閱[執行知識探索](../data-quality-services/perform-knowledge-discovery.md)、[管理定義域](../data-quality-services/managing-a-domain.md)或[建立比對原則](../data-quality-services/create-a-matching-policy.md)。  
  
  
