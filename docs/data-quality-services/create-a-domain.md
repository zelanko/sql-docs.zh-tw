---
title: "建立定義域 | Microsoft Docs"
ms.custom: ""
ms.date: "11/08/2011"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "data-quality-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dqs.kb.createdomain.f1"
ms.assetid: 5c4828f5-bd51-4c29-b3de-87b7d2f2d3e5
caps.latest.revision: 23
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 23
---
# 建立定義域
  此主題描述如何在 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 中建立定義域。 定義域中的值是欄位中資料的語意表示法。 如需有關網域的詳細資訊，請參閱 [管理定義域](../data-quality-services/managing-a-domain.md)。  
  
 建立新的定義域的方式有兩種。 第一種方式是在知識探索活動的對應步驟期間，當您正在分析資料取樣，將知識加入至新的知識庫或現有知識庫時。 第二種方式是在定義域管理活動期間，當您建立新的定義域，而不是變更現有定義域時。  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Prerequisites"></a> 必要條件  
 若要建立定義域，您必須已建立及開啟知識庫。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 您必須擁有 DQS_MAIN 資料庫的 dqs_kb_editor 角色或 dqs_administrator 角色，才能建立定義域。  
  
##  <a name="Discovery"></a> 在知識探索活動中建立定義域  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [執行資料品質用戶端應用程式](../data-quality-services/run-the-data-quality-client-application.md)。  
  
2.  在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 首頁畫面中，按一下 **[開啟知識庫]** ，然後選取知識庫，或是按一下 **[新增知識庫]** ，並輸入新知識庫的屬性。  
  
3.  選取 **[知識探索]** 當做活動，然後按一下 **[建立]** 建立新的知識庫，或按一下 **[開啟]** 開啟現有的知識庫。  
  
4.  在 **[對應]** 頁面上，指定資料來源的連接。 如需詳細資訊，請參閱＜ [Perform Knowledge Discovery](../data-quality-services/perform-knowledge-discovery.md)＞。  
  
5.  在 **對應** 資料表中，從下拉式清單中選取來源資料行 **來源資料行** 空白資料列的資料行。 如果沒有對應的定義域存在，按一下 **建立網域** 圖示。  
  
##  <a name="DomainManagement"></a> 在定義域管理活動中建立定義域  
  
1.  在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 首頁畫面中，按一下 **[開啟知識庫]** ，然後選取知識庫，或是按一下 **[新增知識庫]** ，並輸入新知識庫的屬性。  
  
2.  選取 **[定義域管理]** 當做活動，然後按一下 **[建立]** 建立新的知識庫，或按一下 **[開啟]** 開啟現有的知識庫。  
  
3.  在 **定義域管理** 頁面上，按一下 **建立網域** 定義域清單上方的圖示。  
  
##  <a name="Properties"></a> 設定定義域屬性  
  
1.  在 **建立網域** ] 對話方塊中，輸入知識庫和最多 256 個字元的描述是唯一的名稱。  
  
    > [!NOTE]  
    >  如需有關定義域屬性的詳細資訊，請參閱 [設定網域屬性](../data-quality-services/set-domain-properties.md)。  
  
2.  從 **資料型別** 清單中，選取網域中的資料類型的值。 資料型別可以是 **字串** （預設）、 **日期**, ，**整數**, ，或 **十進位**。  
  
3.  選取 **使用前置值** 指定一組同義字中的前置值將會是輸出，而不是與其同義的值。 取消選取 **使用前置值** ，指定每一個同義字值是正確或更正形式的輸出，而且其群組的前置值不會被取代。  
  
4.  如果資料類型是 **字串**, ，請選取 **將字串標準化** 來移除定義域值，這樣可能會提升相符的可能性中特殊字元。  
  
5.  從 **輸出格式為** 下拉式清單中，選取將套用的格式，當網域中的資料值為輸出。 此格式專屬於步驟 2 中選取的資料類型，如下列清單所示：  
  
    -   如果是字串值，您可以指定字串應該輸出為大寫或小寫。  
  
    -   如果是日期值，您可以指定日、月和年的格式。  
  
    -   如果是整數值，您可以指定要套用之格式遮罩的類型。  
  
    -   如果是十進位值，您可以指定要套用之格式遮罩的精確度和類型。  
  
     選取 **無** 中 **輸出格式為** 下拉式清單，表示不會套用任何清單中的格式。  
  
6.  如果資料類型是 **字串**, ，請在 **語言** 下拉式清單中，選取您要套用，如果您啟用拼字檢查拼字檢查哪一個語言版本。  
  
7.  如果資料類型是 **字串**, ，請選取 **啟用拼字檢查** 擴展定義域時，針對所有字串值執行拼字檢查。  
  
8.  如果資料類型是 **字串**, ，請選取 **停用語法錯誤演算法** 來擴展定義域，而不檢查字串值的語法錯誤。  
  
9. 按一下 **[確定]**。  
  
10. 按一下 **[完成]** ，完成定義域管理活動，如＜ [End the Domain Management Activity](../Topic/End%20the%20Domain%20Management%20Activity.md)＞中所述。  
  
##  <a name="FollowUp"></a> 後續操作：建立定義域之後  
 在建立定義域之後，您可以針對定義域執行其他定義域管理工作、執行知識探索來將知識加入至定義域，或者將比對原則加入至定義域。 如需詳細資訊，請參閱 [執行知識探索](../data-quality-services/perform-knowledge-discovery.md), ，[管理定義域](../data-quality-services/managing-a-domain.md), ，或 [建立比對原則](../data-quality-services/create-a-matching-policy.md)。  
  
  