---
title: 使用全文檢索索引精靈 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
f1_keywords:
- sql12.swb.fulltextindexingwizard.selecttablecolumns.f1
- sql12.swb.fulltextindexingwizard.welcome.f1
- sql12.swb.fulltextindexingwizard.selectacatalog.f1
- sql12.swb.fulltextindexingwizard.progress.f1
- sql12.swb.fulltextindexingwizard.selectorcreatepopschedules.f1
- sql12.swb.fulltextindexingwizard.selectatableorview.f1
- sql12.swb.fulltextindexingwizard.selectchangetracking.f1
- sql12.swb.fulltextindexingwizard.selectanindex.f1
- sql12.swb.fulltextindexingwizard.summary.f1
helpviewer_keywords:
- Full-Text Indexing Wizard
- full-text search [SQL Server], Full-Text Indexing Wizard
ms.assetid: 3e9d9605-6525-4781-9168-fdaa06db3459
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 767c83b5eb6483ca4804e8602886932ff8e40793
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48054298"
---
# <a name="use-the-full-text-indexing-wizard"></a>使用全文檢索索引精靈
  全文檢索索引精靈會提供一系列的逐步說明，以協助您建立全文檢索索引。  
  
#### <a name="to-use-the-full-text-indexing-wizard"></a>使用全文檢索索引精靈  
  
1.  在物件總管中，以滑鼠右鍵按一下您要建立全文檢索索引的資料表、指向 [全文檢索索引]，然後按一下 [Define Full-Text Index (定義全文檢索索引)]。  
  
     **唯一索引**  
     從下拉式清單中選取索引。 索引必須是單一索引鍵資料行、唯一的且不可以是 Null 的索引。 請選取最小的唯一索引鍵索引來當做全文檢索唯一索引鍵。 為求最佳效能，建議使用叢集索引。  
  
     **可用的資料行**  
     若要在索引中包含資料行，請選取資料行名稱旁邊的核取方塊。 不適合全文檢索索引的資料行會以灰色顯示，並會停用其核取方塊。  
  
     **斷詞工具的語言**  
     從下拉式清單中選取語言。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 將使用此選擇來識別索引的正確斷詞工具。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用斷詞工具來識別全文檢索索引資料中的字詞界限。  
  
     **類型資料行**  
     選取資料行的名稱，其中包含要建立全文檢索索引之資料行的文件類型。  
  
     **類型資料行**中命名的資料行時，才會啟用**可用的資料行**sloupec je typu`varbinary(max)`或`image`。  
  
     **統計語意**  
     選取是否要針對選取的資料行啟用語意索引。 如需詳細資訊，請參閱[語意搜尋 &#40;SQL Server&#41;](semantic-search-sql-server.md)。  
  
     如果您在選取 **[統計語意]** 之前選取 **[語言]**，而且選取的語言沒有相關聯的語意語言模型，則會停用 **[統計語意]** 核取方塊。 如果您在選取 [語言] 之前選取 [統計語意]，則下拉式方塊中提供的語言將受限為有語意語言模型支援的語言。  
  
2.  選取變更追蹤選項。  
  
     **自動**  
     選取此選項按鈕，以使基礎資料發生變更時自動更新全文檢索索引。  
  
     **手動**  
     選取此選項按鈕，以使基礎資料發生變更時不會自動更新全文檢索索引。 基礎資料的變更會被保留。 不過，若要將變更套用至全文檢索索引，您必須手動啟動或手動排程此處理序。  
  
     **不要追蹤變更**  
     選取此選項按鈕，以使基礎資料變更時不會更新全文檢索索引。  
  
     **建立索引後啟動完整母體擴展**  
     選取此選項按鈕，以在此精靈順利完成時開始完整母體擴展。 這會由在目錄中建立全文檢索索引結構，然後使用全文檢索索引資料進行擴展來組成。  
  
3.  選取目錄、索引檔案群組和停用字詞表。  
  
     **選取全文檢索目錄**  
     從清單中選取全文檢索目錄。 資料庫的預設目錄是清單中預設選取的項目。 如果沒有任何目錄可以使用，系統就會停用此清單，而且會核取及停用 **[建立新的目錄]** 核取方塊。  
  
    |||  
    |-|-|  
    |**[建立新的目錄]**|選取即可建立新的全文檢索目錄。|  
  
     **名稱**  
     輸入新的全文檢索目錄的名稱。  
  
     **設定為預設目錄**  
     選取即可讓此目錄成為這個資料庫的預設目錄。  
  
     **區分腔調字**  
     指定新目錄是要區分腔調字或不區分腔調字。 如果資料庫有區分腔調字，預設就會選取 [區分]。  
  
     **選取索引檔案群組**  
     指定要在上面建立全文檢索索引的檔案群組。  
  
     選取下列其中一個值：  
  
    |值|描述|  
    |-----------|-----------------|  
    |**\<預設值 >**|如果資料表或檢視未分割，請選取此值，以便與基礎資料表或檢視使用的相同檔案群組。 如果資料表或檢視表已分割，則會使用主要檔案群組。|  
    |**PRIMARY**|選取即可針對新的全文檢索索引使用主要檔案群組。|  
    |*使用者指定的預設檔案群組*|如果使用者定義的預設停用字詞表已存在，請從清單中選取其名稱，以便針對新的全文檢索索引使用該檔案群組。|  
  
     **選取全文檢索停用字詞表**  
     指定要針對全文檢索索引使用的停用字詞表，或停用停用字詞表。  
  
     在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 及更新的版本中，停用字詞在資料庫中是使用稱為停用字詞表的物件來管理。 「停用字詞表」是停用字詞的清單，與全文檢索索引相關聯時，會套用至該索引上的全文檢索查詢。 如需詳細資訊，請參閱 [設定及管理全文檢索搜尋的停用字詞與停用字詞表](configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)。  
  
     選取下列其中一個值：  
  
    |值|描述|  
    |-----------|-----------------|  
    |**\<系統 >**|選取即可針對新的全文檢索索引使用系統停用字詞表。 這是預設值。|  
    |**\<關閉 >**|選取即可針對新的全文檢索索引停用停用字詞表。|  
    |*user-defined-stoplist-name*|此清單會顯示已經在資料庫上建立之每個使用者定義停用字詞表的名稱 (如果有的話)。 選取要針對新的全文檢索索引使用的任何使用者定義停用字詞表。|  
  
4.  選擇性地定義母體擴展排程。 除非索引作業已排程於未來執行，否則會立即開始索引作業。 排程本身會立即建立，不過要等排程時間到了才會執行。  
  
     **新增資料表排程**  
     定義資料表的母體擴展排程。  
  
     **新增目錄排程**  
     定義全文檢索目錄的母體擴展排程。  
  
     **編輯**  
     編輯排程。  
  
     **刪除**  
     刪除排程。  
  
5.  檢視或控制全文檢索索引精靈的進度。  
  
     **停止**  
     中斷目前的作業，並防止精靈在此工作階段期間執行後續的全文檢索作業。  
  
     **報表**  
     當所有作業都執行完成後，按一下此按鈕以存取所執行作業的報表。 您可以檢視報表、將其列印至檔案、將其複製到剪貼簿或以電子郵件傳送報表。  
  
  
