---
title: 設定定義域屬性 | Microsoft Docs
ms.custom: ''
ms.date: 11/08/2011
ms.prod: sql-non-specified
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
- sql13.dqs.dm.domainproperties.f1
ms.assetid: 8a3c88ca-31d6-4f75-9aca-cf027c6d9845
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 522b09e704b6536d5b2748dae71fd2710a664b9e
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/18/2018
---
# <a name="set-domain-properties"></a>設定定義域屬性

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  此主題描述如何在 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 中設定定義域屬性。  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Prerequisites"></a> 必要條件  
 若要為定義域設定屬性，您必須已建立知識庫和定義域。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
 您必須擁有 DQS_MAIN 資料庫的 dqs_kb_editor 角色或 dqs_administrator 角色，才能設定定義域的屬性。  
  
##  <a name="Set"></a> 設定定義域屬性  
  
1.  若要設定現有定義域的屬性，請在 [定義域管理] 活動中開啟知識庫 (請參閱＜ [Open a Knowledge Base](../data-quality-services/open-a-knowledge-base.md)＞)，然後在 **[定義域]** 清單中選取適當的定義域。 預設會顯示 [定義域屬性] 頁面。  
  
2.  在建立新的定義域之後設定其屬性，如＜ [Create a Domain](../data-quality-services/create-a-domain.md)＞中所述。  
  
3.  按一下 **[完成]** ，完成定義域管理活動，如＜ [結束定義域管理活動](http://msdn.microsoft.com/library/ab6505ad-3090-453b-bb01-58435e7fa7c0)＞中所述。  
  
##  <a name="FollowUp"></a> 後續操作：設定定義域屬性之後  
 在您設定定義域屬性之後，您可以針對定義域執行其他定義域管理工作、執行知識探索來將知識加入至定義域，或者將比對原則加入至定義域。 如需詳細資訊，請參閱[執行知識探索](../data-quality-services/perform-knowledge-discovery.md)、[管理定義域](../data-quality-services/managing-a-domain.md)或[建立比對原則](../data-quality-services/create-a-matching-policy.md)。  
  
##  <a name="Properties"></a> 定義域屬性  
  
###  <a name="Name"></a> 定義域名稱和描述  
 建立定義域之後，可以變更定義域名稱或描述。 定義域名稱在知識庫中必須是唯一的。 描述最多可以有 256 個字元。  
  
###  <a name="Type"></a> 資料類型  
 當您建立定義域時，請針對定義域中的值選取下列其中一個資料類型： **[字串]** (預設值)、 **[日期]**、 **[整數]** 或 **[十進位]**。 在您建立定義域之後，可以檢視資料類型，但是無法變更資料類型。 針對定義域所選取的資料類型會定義可對應至該定義域的來源資料類型。 如需 DQS 中四種定義域資料類型分別支援之資料類型的資訊，請參閱 [DQS 定義域支援的 SQL Server 和 SSIS 資料類型](../data-quality-services/supported-sql-server-and-ssis-data-types-for-dqs-domains.md)。  
  
###  <a name="Leading"></a> 使用前置值  
 選取這個核取方塊，指定一組同義字中的前置值將會是輸出，而不是與其同義的值。 取消選取 **[使用前置值]** ，指定每一個同義字值都是正確或更正形式的輸出，而且不會由其群組的前置值加以取代。  
  
###  <a name="Normalize"></a> 正在將字串標準化  
 如果資料類型是 **[字串]**，請按一下以忽略來源資料中的特殊字元，以便 DQS 進行資料品質處理。 DQS 內部會在資料載入至網域時，以 null 或空格取代特殊字元。 冒號、連字號、句號、雙引號或分號會由空格取代。 單引號會由 null 取代。 使用 null 會將字串的兩部分結合在一起。  
  
 忽略字串值內的特殊字元可提高比對精確度。 若要增加兩個字串之間的相似度分數，可以使用 null 或空格取代特殊字元。 標點符號或其他符號在其他字串中可以很輕易地不同。 由內部取代特殊字元可讓分數超過 DQS 的最低比對臨界值，讓兩個原本不會相符的字串被視為相符。 但是，您是否選擇忽略特殊字元可能取決於您執行比對所針對的資料類型。 例如，當您處理英制度量系統的資料時，如果雙引號代表英吋且單引號代表英呎，則忽略產品資料中的雙引號和單引號可能會造成誤判。  
  
 在探索、比對原則、比對專案和清理專案活動的資料處理階段載入資料及建立資料索引時，將會執行正規化。 如果啟用的話，正規化和以詞彙為主的關聯轉換都會在前置處理階段執行，然後再進行分析。 這些作業會先在每一個定義域上執行，然後才會套用計算兩個字串之間之相似度的任何演算法。 如果要求複合定義域剖析，則會在正規化和以詞彙為主的關聯轉換之前執行，因為分隔符號剖析需要符號。 其他作業 (例如定義域規則和定義域值變更) 將會在轉換之後執行。 DQS 內部取代特殊字元並不會變更結果資料。  
  
###  <a name="Format"></a> 設定輸出格式為  
 選取當定義域中的資料值為輸出時，將套用的格式。 此格式是選取的資料類型所特有，如下列清單所示。 選取 **[無]** 表示不會套用清單中的任何格式。  
  
-   如果是字串值，您可以指定字串應該輸出為大寫或小寫。  
  
-   如果是日期值，您可以指定日、月和年的格式。  
  
-   如果是整數值，您可以指定要套用之格式遮罩的類型。  
  
-   如果是十進位值，您可以指定要套用之格式遮罩的精確度和類型。  
  
###  <a name="Language"></a> 語言  
 如果資料類型是 **[字串]**，請選取您希望將哪一種語言與定義域產生關聯，以進行拼字檢查作業。 這個選取項目只適用於拼字檢查，因為拼字檢查結果取決於使用中的語言。 此選取項目只適用於資料類型為字串的單一定義域。 對於複合定義域而言，語言屬性是不相關的。 複合定義域之每一個部分的語言都是由相關的單一定義域所決定。  
  
 預設語言為英文。 將 **[語言]** 屬性設定為 **[其他]** 會停用定義域的拼字檢查。  
  
> [!TIP]  
>  如果 **[語言]** 下拉式清單中未列出您的語言，則必須選取 **[其他]**。 這樣可確保 DQS 根據定義域中的可用知識 (定義域規則、定義域值、TBR、比對規則) 清理並刪除未列出之語言資料的重複項目。  
  
###  <a name="Speller"></a> 啟用拼字檢查  
 如果資料類型是 **[字串]**，按一下此選項可為定義域啟用 DQS 拼字檢查。 拼字檢查只適用於資料類型為字串的定義域。 **[啟用拼字檢查]** 核取方塊只會針對與此核取方塊相關聯的單一定義域來啟用拼字檢查。 此核取方塊不適用於複合定義域。  
  
 拼字檢查會針對定義域中的值來建議語法和驗證更正。 如需詳細資訊，請參閱＜ [Use the DQS Speller](../data-quality-services/use-the-dqs-speller.md)＞。  
  
###  <a name="Syntax"></a> 停用語法錯誤演算法  
 如果資料類型是 **[字串]**，選取此選項可指定定義域中的 DQS 在清理期間將不會識別語法錯誤。 當識別該定義域的語法錯誤無關緊要時，請選取這個核取方塊。 例如，對序號識別語法錯誤可能無關緊要。 此控制項只適用於字串資料類型。 DQS 將不會檢查非字串資料類型的語法錯誤。  
  
  
