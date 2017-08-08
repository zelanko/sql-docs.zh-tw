---
title: "使用全文檢索索引精靈 | Microsoft 文件"
ms.custom: 
ms.date: 08/19/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-search
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.fulltextindexingwizard.welcome.f1
- sql13.swb.fulltextindexingwizard.selectorcreatepopschedules.f1
- sql13.swb.fulltextindexingwizard.progress.f1
- sql13.swb.fulltextindexingwizard.selectchangetracking.f1
- sql13.swb.fulltextindexingwizard.selectacatalog.f1
- sql13.swb.fulltextindexingwizard.selectatableorview.f1
- sql13.swb.fulltextindexingwizard.selectanindex.f1
- sql13.swb.fulltextindexingwizard.summary.f1
- sql13.swb.fulltextindexingwizard.selecttablecolumns.f1
helpviewer_keywords:
- Full-Text Indexing Wizard
- full-text search [SQL Server], Full-Text Indexing Wizard
ms.assetid: 3e9d9605-6525-4781-9168-fdaa06db3459
caps.latest.revision: 24
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 439b568fb268cdc6e6a817f36ce38aeaeac11fab
ms.openlocfilehash: 204b0e834db9ad1c5fe7d3f08f507629313e3cad
ms.contentlocale: zh-tw
ms.lasthandoff: 07/31/2017

---
# <a name="use-the-full-text-indexing-wizard"></a>使用全文檢索索引精靈
  SSMS 中的 [全文檢索索引精靈] 會提供一系列的逐步說明，以協助您建立全文檢索索引。  
  
## <a name="create-a--full-text-index"></a>建立全文檢索索引 

1. 在物件總管中，以滑鼠右鍵按一下您要建立全文檢索索引的資料表、指向 [全文檢索索引]，然後按一下 [Define Full-Text Index (定義全文檢索索引)]。 這個動作會在另一個視窗中啟動精靈。
   按 [下一步] 
  
2. **唯一索引。**  從下拉式清單中選取索引。 索引必須是單一索引鍵資料行、唯一的且不可以是 Null 的索引。 請選取最小的唯一索引鍵索引來當做全文檢索唯一索引鍵。 為求最佳效能，建議使用叢集索引。  
  
3.  **可用的資料行。** 請核取您想要包含之資料行的所有資料行名稱旁邊的方塊。  資料行名稱旁邊的核取方塊。 不適合資料行會變成灰色，並停用其核取方塊。  
  
4. **斷詞工具的語言。** 從下拉式清單中選取語言。 將使用這個選項來識別索引的正確斷詞工具。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用斷詞工具來識別全文檢索索引資料中的字詞界限。  
  
5.  **類型資料行。** 選取資料行的名稱，其中包含要建立全文檢索索引之資料行的文件類型。  
> **注意：**只有在 [可用的資料行] 資料行中命名的資料行類型為 **varbinary(max)** 或 **image** 時，才會啟用 [類型資料行]。  
  
6. **統計語意。** 選取是否要針對選取的資料行啟用語意索引。 如需詳細資訊，請參閱[語意搜尋 &#40;SQL Server&#41;](../../relational-databases/search/semantic-search-sql-server.md)。  
  
>**注意** 
>
>如果您選取的語言沒有相關聯的語意語言模型，則不會啟用 [統計語意] 核取方塊。 如果您在選取 [語言] 之前選取 [統計語意]，則下拉式方塊中提供的語言將受限為有語意語言模型支援的語言。  
>
> **Azure SQL Database 無法使用**語意搜尋。 在 Azure SQL Database 上執行此精靈時，不會出現 [統計語意] 選項。
  
7. 選取變更追蹤選項。  
  
     **自動**  
     選取此選項按鈕，以使基礎資料發生變更時自動更新全文檢索索引。  
  
     **手動**  
     選取此選項按鈕，以使基礎資料發生變更時不會自動更新全文檢索索引。 基礎資料的變更會被保留。 不過，若要將變更套用至全文檢索索引，您必須手動啟動或手動排程此處理序。  
  
     **不要追蹤變更**  
     選取此選項按鈕，以使基礎資料變更時不會更新全文檢索索引。  
  
8.  建立索引後啟動完整母體擴展 (只適用於您不要追蹤變更時)。
  
     選取此選項按鈕，以在此精靈順利完成時開始完整母體擴展。 這會由在目錄中建立全文檢索索引結構，然後使用全文檢索索引資料進行擴展來組成。  
     
     按 [下一步]
  
## <a name="catalog-index-filegroup-and-stoplist"></a>目錄、索引檔案群組和停用字詞表   
  
9.  **選取全文檢索目錄**  

     **選取目錄：** 從清單中選取全文檢索目錄。 資料庫的預設目錄是清單中預設選取的項目。 如果沒有任何目錄可以使用，系統就會停用此清單，而且會核取及停用 **[建立新的目錄]** 核取方塊。  
  
  OR
  
 10. **[建立新的目錄]**
 - 選取全文檢索目錄。  
  
    a. **名稱**  
     輸入新全文檢索目錄的名稱。  
  
     b. **設定為預設目錄**  
     選取即可讓此目錄成為這個資料庫的預設目錄。  
  
     c. **區分腔調字**  
     指定新目錄是要區分腔調字或不區分腔調字。 如果資料庫區分腔調字，預設會選取 [區分]。  
  
     d. **選取索引檔案群組**  
     指定要在上面建立全文檢索索引的檔案群組。  
  
     E. 選取值：  
      |Value|描述|  
      |-----------|-----------------|
      |**<default>**| 如果資料表或檢視未分割，請選取此值，以便與基礎資料表或檢視使用的相同檔案群組。 如果已分割資料表或檢視表，則會使用主要檔案群組|
      |**PRIMARY**|選取即可針對新的全文檢索索引使用主要檔案群組。|
      *使用者指定的預設檔案群組*|如果使用者定義的預設停用字詞表已存在，請從清單中選取其名稱，以便針對新的全文檢索索引使用該檔案群組。|   
  
     
 11. **選取全文檢索停用字詞表**  
     指定要針對全文檢索索引使用的停用字詞表，或停用停用字詞表。  
  
     資料庫中的停用字詞是使用稱為停用字詞表的物件來管理。 「停用字詞表」是停用字詞的清單，與全文檢索索引相關聯時，會套用至該索引上的全文檢索查詢。 如需詳細資訊，請參閱[設定及管理全文檢索搜尋的停用字詞與停用字詞表](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)。  
  
     選取下列其中一個值：  
  
   |Value|描述|  
    |-----------|-----------------|  
    |**<system>**|選取即可針對新的全文檢索索引使用系統停用字詞表。 這是預設值。|  
    |**<off>**|選取即可針對新的全文檢索索引停用停用字詞表。|  
    |*user-defined-stoplist-name*|此清單會顯示已經在資料庫上建立之每個使用者定義停用字詞表的名稱 (如果有的話)。 選取要針對新的全文檢索索引使用的任何使用者定義停用字詞表。|  
  
  按 [下一步]
  
11. 選擇性地定義母體擴展排程 (僅限 SQL Server)。 除非索引作業已排程於未來執行，否則會立即開始索引作業。 排程本身會立即建立，不過要等排程時間到了才會執行。  
  
     **新增資料表排程**  
     定義資料表的母體擴展排程。  
  
     **新增目錄排程**  
     定義全文檢索目錄的母體擴展排程。  
  
     **編輯**  
     編輯排程。  
  
     **Delete**  
     刪除排程。  
  
5.  檢視或控制全文檢索索引精靈的進度。  
  
     **停止**  
     中斷目前的作業，並防止精靈在此工作階段期間執行後續的全文檢索作業。  
  
     **報表**  
     當所有作業都執行完成後，按一下此按鈕以存取所執行作業的報表。 您可以檢視報表、將其列印至檔案、將其複製到剪貼簿或以電子郵件傳送報表。  
  
  

