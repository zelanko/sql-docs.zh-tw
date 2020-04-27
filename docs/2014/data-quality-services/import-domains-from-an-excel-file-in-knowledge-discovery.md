---
title: 將 Excel 檔案中的定義域匯入知識探索 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 4d3a3940-6c2a-4dc4-90eb-86f26012c165
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 0ca7391a025cf0fe4477cc9008c51c0a06a59f00
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "65480539"
---
# <a name="import-domains-from-an-excel-file-in-knowledge-discovery"></a>在知識探索中匯入 Excel 檔案中的定義域
  此主題描述如何在 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 知識探索活動中匯入 Excel 檔案中的一個或多個定義域。 此匯入程序會簡化知識產生程序，以節省時間和精力。 此程序可讓擁有 Excel 檔案或文字檔資料的人建立包含該資料的知識庫 （如需將值匯入現有知識庫定義域的詳細資訊，請參閱將[Excel 檔案中的值](../../2014/data-quality-services/import-values-from-an-excel-file-into-a-domain.md)匯入定義域。）不支援匯出至 Excel 檔案。  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> 必要條件  
 若要從 Excel 檔案匯入定義域，安裝 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 的電腦上必須已安裝 Excel；您必須已經使用定義域值建立 Excel 檔案 (請參閱 [How the import works](#How))；而且您必須已經建立及開啟要匯入定義域到其中的知識庫。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 您必須擁有 DQS_MAIN 資料庫的 dqs_kb_editor 角色或 dqs_administrator 角色，才能從 Excel 檔案匯入定義域。  
  
##  <a name="import-domains-from-an-excel-file-into-a-knowledge-base"></a><a name="Import"></a> 將 Excel 檔案中的定義域匯入知識庫  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][執行 Data Quality Client 應用程式](../../2014/data-quality-services/run-the-data-quality-client-application.md)。  
  
2.  在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 首頁畫面中，執行下列其中一項作業：  
  
    -   若要建立新的知識庫，以便將資料匯入其中，請按一下 **[新增知識庫]**、輸入知識庫的名稱、為 **[建立知識庫來源]** 選取 **[無]**、選取 **[知識探索]** 活動，然後按一下 **[建立]**。  
  
    -   若要開啟現有知識庫，以便將資料匯入其中，請按一下 **[開啟知識庫]**、選取知識庫、選取 **[知識探索]**，然後按 **[下一步]**。  
  
3.  在 [對應] **** 頁面上，針對 [資料來源] **** 選取 [Excel 檔案] ****。  
  
4.  在 **[Excel 檔案]** 行上按一下 **[瀏覽]** 。  
  
5.  在 **[選取 Excel 檔案]** 對話方塊中，移至您想要匯入之來源 Excel 檔案所在的資料夾，並選取此 Excel 檔案，然後按一下 **[開啟]**。  
  
6.  從 **[工作表]** 下拉式清單中，選取您想要匯入之來源 Excel 檔案中的工作表。  
  
7.  如果您希望第一個資料列被視為資料標頭，而且您希望第一個資料列中的值當做資料行名稱使用，請選取 **[使用第一個資料列做為標頭]** 。 如果您希望第一個資料列被視為資料值，此時 DQS 會將 Excel 標頭名稱 (英文字母) 用於資料行，請取消選取 **[使用第一個資料列做為標頭]** 。  
  
8.  選取資料行，然後將現有的定義域對應至此資料行，或是建立新的定義域，方法是按一下 **[建立定義域]** 圖示、在 **[建立定義域]** 對話方塊中建立定義域，然後將此定義域對應至此資料行。 此定義域的資料類型必須符合此資料行的資料類型。 針對試算表的所有資料行重複上述步驟。  
  
9. 按 [下一步]  。  
  
10. 在 **[探索]** 頁面上，按一下 **[開始]** ，分析 Excel 試算表中的資料。  
  
    > [!NOTE]  
    >  如果您在資料上傳完畢之前離開頁面，檔案上傳程序將會終止。  
  
11. 確認分析已順利完成，然後按 **[下一步]**。  
  
12. 在 **[管理定義域值]** 頁面中，確認正確的定義域已列在 **[定義域]** 清單中，而且值已輸入定義域資料表中。  
  
13. 按一下 **[完成]**，然後按一下 **[發行]** 發行知識庫，或是按一下 **[否]** ，不發行。  
  
14. 確認知識庫已發行，然後按一下 **[確定]**。  
  
##  <a name="follow-up-after-importing-domains-from-an-excel-file"></a><a name="FollowUp"></a>後續操作：從 Excel 檔案匯入定義域之後  
 當您從 Excel 檔案匯入定義域之後，您可以將知識加入至定義域，或是在清理或比對專案時使用定義域 (根據定義域的內容而定)。 如需詳細資訊，請參閱[執行知識探索](../../2014/data-quality-services/perform-knowledge-discovery.md)、[管理定義域](../../2014/data-quality-services/managing-a-domain.md)、[管理複合定義域](../../2014/data-quality-services/managing-a-composite-domain.md)、[建立比對原則](../../2014/data-quality-services/create-a-matching-policy.md)、[資料清理](../../2014/data-quality-services/data-cleansing.md)或[資料比對](../../2014/data-quality-services/data-matching.md)。  
  
##  <a name="how-the-import-works"></a><a name="How"></a>匯入的運作方式  
 在匯入作業中，DQS 會依照以下方式解譯 Excel 檔案：  
  
-   資料行表示定義域  
  
-   資料列表示資料記錄  
  
-   第一個資料列表示定義域名稱，或者為第一個資料值或記錄 (根據 **[使用第一個資料列做為標頭]** 核取方塊的設定而定)。  
  
 下列規則適用於匯入作業：  
  
-   這個作業會將定義域值匯入知識庫中， 而不會匯入定義域規則或比對原則。  
  
-   Excel 檔案的副檔名可為 .xlsx、.xls 或 .csv。 要匯入定義域值或完整定義域的 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 電腦上必須安裝 Microsoft Excel。 Excel 2003 及更新的版本都有受到支援。 如果使用 64 位元版本的 Excel，則僅支援 Excel 2003 檔案；Excel 2007 或 2010 檔案將不受支援。  
  
-   Excel 64 位元安裝不支援 Excel 檔案類型 .xlsx。 如果您使用 64 位元 Excel，請將試算表檔案儲存為 .xls 檔案。  
  
-   在 .xlsx 和 .xls 檔案中，資料行的資料類型是由前八個資料列中最普遍的資料類型所決定。 如果資料格不符合該資料類型，將會為它提供 null 值。  
  
-   在 .csv 檔案中，資料類型是由前八個資料列中最普遍的資料類型所決定。  
  
-   如果 Excel 試算表中的值不符合定義域規則，則會將它匯入為無效的值。  
  
-   如果 Excel 檔案的格式不正確或是已損毀，則匯入作業會產生錯誤。  
  
  
