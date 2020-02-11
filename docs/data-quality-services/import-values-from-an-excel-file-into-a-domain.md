---
title: 將 Excel 檔案中的值匯入定義域中
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql13.dqs.kb.importfailing.f1
- sql13.dqs.kb.importselect.f1
- sql13.dqs.kb.failingvalues.f1
ms.assetid: 04cde693-2043-477f-8417-fcc463ca7195
author: swinarko
ms.author: sawinark
ms.openlocfilehash: 144a2b57fa671842f284445dee859e689e8adbe1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "75254822"
---
# <a name="import-values-from-an-excel-file-into-a-domain"></a>將 Excel 檔案中的值匯入定義域中

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  本主題描述如何將 Excel 檔案中的值匯入 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 的定義域中。 使用 Excel 檔案將定義域值匯入 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 應用程式可簡化知識產生程序，進而節省時間與精力。 此程序可讓在 Excel 檔案或文字檔案中擁有有效資料值清單的人，將這些值匯入定義域中。 透過 Excel 檔案，您可以將定義域值匯入定義域或將定義域匯入知識庫中 （如需將定義域匯入知識庫的詳細資訊，請參閱[在知識探索中匯入 Excel 檔案中的定義域](../data-quality-services/import-domains-from-an-excel-file-in-knowledge-discovery.md)）。不支援匯出至 Excel 檔案。  
  
 您可以用兩種方式匯入資料值：  
  
-   建立新的定義域，然後從 Excel 檔案將值匯入定義域中，此時所有值都會加入至定義域。  
  
-   將值匯入現有且已填入的定義域中，此時只會匯入新的值。 系統將不會匯入已經存在的所有值。  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Prerequisites"></a> 必要條件  
 若要從 Excel 檔案匯入定義域，安裝 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 應用程式的電腦上必須已安裝 Excel，才能匯入定義域值或完整定義域；您必須已經使用定義域值建立 Excel 檔案 (請參閱＜ [How the import works](#How)＞)；而且您必須已經建立及開啟要匯入定義域到其中的知識庫。  
  
###  <a name="Security"></a> Security  
  
####  <a name="Permissions"></a> 權限  
 您必須擁有 DQS_MAIN 資料庫的 dqs_kb_editor 或 dqs_administrator 角色，才能從 Excel 檔案匯入定義域值。  
  
##  <a name="Import"></a>將 Excel 檔案中的值匯入定義域中  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][執行 Data Quality Client 應用程式](../data-quality-services/run-the-data-quality-client-application.md)。  
  
2.  在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 首頁畫面中，於 [定義域管理] 活動中開啟知識庫。  
  
3.  如果您要將值加入至新的定義域，請使用 **[建立定義域]** 圖示來建立新的定義域，然後在定義域清單中選取新的定義域。  
  
4.  如果您要將值加入至現有的定義域，請在定義域清單中選取定義域。  
  
5.  按一下 **[定義域值]** 索引標籤、按一下圖示列中的 **[匯入值]** 圖示，然後按一下 **[從 Excel 匯入有效值]**。  
  
6.  在 **[匯入定義域值]** 對話方塊中，按一下 **[瀏覽]**。  
  
7.  在 **[選取檔案]** 對話方塊中，移至您想要匯入定義域值之來源 Excel 檔案所在的資料夾、選取此檔案 (副檔名為 .xlsx、.xls 或 .csv)，然後按一下 **[開啟]**。 此檔案必須位於您從中執行 DQS 的用戶端上，或位於使用者擁有存取權的共用檔案中。  
  
8.  在 **[工作表]** 下拉式清單中，選取您要匯入的來源工作表。  
  
9. 如果試算表中的第一個資料列代表定義域名稱，而且所有其他資料列都代表有效的定義域值，請選取 **[使用第一個資料列做為標頭]** 。  
  
10. 按一下 [確定]  。 此時，系統會顯示進度列，其中指出已經成功匯入的值數目、未匯入的數目，以及值的總數。 按一下 **[取消]** 按鈕即可取消進度。  
  
11. 確認「匯入完成」已顯示在 [匯入定義域值]**** 對話方塊中。 您可以在此對話方塊中查看已成功匯入的值，以及未匯入的值。 它會指出檔案的名稱和檔案的路徑、作業的完成狀態、已經成功匯入的值數目、未匯入的值數目，以及已處理的值總數。  
  
12. 對於未成功匯入的這些值，請按一下 [記錄檔]**** 顯示 [匯入定義域值 - 失敗值]**** 對話方塊，以便查看匯入作業失敗的原因。 
  **[失敗值]** 資料行會顯示無法從 Excel 檔案匯入定義域的值，而 **[原因]** 資料行會說明匯入失敗的原因。 您可以按一下 **[複製至剪貼簿]** ，將 **[失敗值]** 資料表複製到 [剪貼簿]，以便將該資料表複製到另一個程式，例如 Excel 試算表或 [記事本] 檔案。 按一下 **[確定]** 關閉 **[失敗值]** 對話方塊。  
  
13. 按一下 **[確定]** 完成匯入作業，然後關閉對話方塊。 當匯入成功完成時， **[定義域值]** 頁面上的定義域值清單就會重新整理，而且將包含新匯入的值。 此時，篩選會變更為 **[所有值]** ，並且選取 **[只顯示新值]** 。 在匯入作業之後選取 **[只顯示新值]** 時，就只會顯示從 Excel 檔案匯入的值。  
  
14. 按一下 **[完成]** ，將值加入至知識庫。  
  
##  <a name="FollowUp"></a>後續操作：將 Excel 檔案中的值匯入定義域之後  
 將值匯入定義域之後，您可以針對定義域執行其他定義域管理工作、執行知識探索以將知識加入至定義域，或者將比對原則加入至定義域。 如需詳細資訊，請參閱[執行知識探索](../data-quality-services/perform-knowledge-discovery.md)、[管理定義域](../data-quality-services/managing-a-domain.md)或[建立比對原則](../data-quality-services/create-a-matching-policy.md)。  
  
##  <a name="Synonyms"></a>匯入同義字  
 同義字的匯入方式如下：  
  
-   首先，系統會匯入所有值，然後建立同義字連接。  
  
-   如果無法連接同義字值，記錄畫面就會顯示錯誤。 檔案中的前置值和同義字可能將匯入定義域，但是不會設定為同義字。  
  
 下列規則適用於設定同義字連接的程序：  
  
-   如果 Excel 檔案中的前置值已經存在定義域中做為不同值的同義字，您就必須手動設定同義字 (例如，在 Excel 檔案中，我們想要讓 A 值成為 B 值的前置值，但是在定義域中，A 值顯示成 C 值的同義字)。 除了在匯入完成之後手動設定同義字以外，您也可以取消連結目前是同義字的值 (例如，取消連結上述 A 和 C 值)，然後再匯入檔案。  
  
-   如果同義字已經連接到不同的前置值，您就必須手動設定同義字。  
  
-   如果由於任何原因而無法在應用程式中手動連接值，表示該值可能不適用於匯入作業。  
  
##  <a name="How"></a>匯入的運作方式  
 此作業將匯入下列值：  
  
 在匯入作業中，DQS 會依照以下方式從 Excel 檔案匯入資料：  
  
-   匯入正確的值和新值。 如果一個或多個匯入的定義域值已經存在，就不會匯入這些值。  
  
-   與定義域規則衝突的值將匯入成無效的值。  
  
-   如果某個值不屬於定義域的資料類型或為 Null，就不會從檔案匯入該值。  
  
-   系統會依照值出現在檔案中的順序匯入值。  
  
-   每個資料列都代表一個定義域值。  
  
-   第一個資料列表示定義域名稱，或者為第一個資料值或記錄 (根據 **[使用第一個資料列做為標頭]** 核取方塊的設定而定)。 如果您在使用 .xslx 或 .xls 檔案時選取 **[使用第一個資料列做為標頭]** ，任何 Null 資料行名稱都將自動轉換成 F*n*，而且任何重複的資料行都會附加一個數字。  
  
-   如果您在匯入作業完成之前加以取消，系統將回復此作業，而且不會匯入任何資料。  
  
-   第一個資料行中的值會匯入定義域中。 如果除了第一個資料行以外，已填入一個或多個其他資料行，則這些資料行中的值將會加入成為同義字 (請參閱＜ [匯入同義字](#Synonyms)＞)。  
  
    -   預期的格式如下：第一個資料行成為前置值，而第二個以上的資料行則成為同義字。  
  
    -   您可以在相同的資料列或不同的資料列中匯入多個同義字。 例如，如果您想要匯入 "NYC" 和 "New York City" 成為 "New York" 的同義字，可以匯入資料行 1 包含 "New York"、資料行 2 包含 "NYC" 而且資料行 3 包含 "New York City" 的單一資料列。或者，您也可以匯入資料行 1 包含 "New York" 而且資料行 2 包含 "NYC" 的一個資料列，以及資料行 1 包含 "New York" 而且資料行 2 包含 "New York City" 的另一個資料列。 請注意，如果 "New York" 值已經存在定義域中，系統就只會加入同義字，而且使用者不會在匯入程序期間收到錯誤，指出該值已經存在。 如果第一個值原本不存在，它就會加入至定義域。  
  
 下列規則適用於針對匯入所使用的 Excel 檔案：  
  
-   Excel 檔案的副檔名可為 .xlsx、.xls 或 .csv。 安裝 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 應用程式電腦上必須安裝 Microsoft Excel，才能匯入定義域值或完整定義域。 Excel 2003 及更新的版本都有受到支援。 如果使用 64 位元版本的 Excel，則僅支援 Excel 2003 檔案，不支援 Excel 2007 或 2010 檔案。  
  
-   Excel 64 位元安裝不支援 Excel 檔案類型 .xlsx。 如果您要使用 64 位元 Excel，請將試算表檔案儲存成 .xls 檔案或 .csv 檔案，或是改為安裝 Excel 32 位元版本。  
  
-   在 .xlsx 和 .xls 檔案中，資料行的資料類型是由前八個資料列所決定。 如果前八個資料列的資料行類型為混合式，資料行類型就是字串。 如果資料列 9 以上的資料格不符合該資料類型，將會為它提供 Null 值。  
  
-   在 .csv 檔案中，資料類型是由前八個資料列中最普遍的資料類型所決定。  
  
-   如果 Excel 檔案的格式不正確或是已損毀，則匯入作業會產生錯誤。  
  
  
