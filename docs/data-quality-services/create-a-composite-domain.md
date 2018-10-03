---
title: 建立複合定義域 | Microsoft Docs
ms.custom: ''
ms.date: 11/22/2011
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology:
- data-quality-services
ms.topic: conceptual
f1_keywords:
- sql13.dqs.kb.createcd.f1
- sql13.dqs.dm.cdproperties.f1
ms.assetid: c7f0bd84-a02e-4a81-885d-985e6415c499
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 4efd1769b95a43b6718eaa635273458bc241f282
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47776600"
---
# <a name="create-a-composite-domain"></a>建立複合定義域

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  此主題描述如何在 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 中的知識庫內建立複合定義域。 複合定義域是由套用至單一資料欄位的一個或多個單一定義域所組成。 如需複合定義域的詳細資訊，請參閱[管理複合定義域](../data-quality-services/managing-a-composite-domain.md)。  
  
 建立新的複合定義域的方式有兩種。 第一種方式是在知識探索活動的對應步驟期間，當您正在分析資料取樣，將知識加入至新的知識庫或現有知識庫時。 第二種方式是在定義域管理活動期間，當您建立新的定義域，而不是變更現有定義域時。 為了建立複合定義域，您至少必須已經建立兩個單一定義域，以便將其加入至複合定義域。 當您建立新的複合定義域時，只有已經建立而且尚未加入至現有複合定義域的單一定義域才可使用。 單一定義域不能加入至一個以上的複合定義域，而且複合定義域不能加入至另一個複合定義域。  
  
 在您建立複合定義域之後，可以變更複合定義域的屬性、將參考資料服務附加至定義域、建立跨定義域規則或建立值關聯。 若要這樣做，請在 **[定義域管理]** 頁面的 **[定義域]** 清單中選取複合定義域，然後選取適當的索引標籤。  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Prerequisites"></a> 必要條件  
 為了建立複合定義域，您必須已經建立及開啟知識庫，而且至少已經建立兩個單一定義域，以便將其加入至複合定義域。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
 您必須擁有 DQS_MAIN 資料庫的 dqs_kb_editor 角色或 dqs_administrator 角色，才能建立複合定義域。  
  
##  <a name="ParsingKnowledgeDiscoveryActivity"></a> 在知識探索活動中建立複合定義域  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [執行 Data Quality Client 應用程式](../data-quality-services/run-the-data-quality-client-application.md)。  
  
2.  在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 首頁畫面中，按一下 **[開啟知識庫]** ，然後選取知識庫，或是按一下 **[新增知識庫]** ，並輸入新知識庫的屬性。  
  
3.  選取 **[知識探索]** 當做活動，然後按一下 **[建立]** 建立新的知識庫，或按一下 **[開啟]** 開啟現有的知識庫。  
  
4.  在 **[對應]** 頁面上，指定資料來源的連接。 如需詳細資訊，請參閱＜ [Perform Knowledge Discovery](../data-quality-services/perform-knowledge-discovery.md)＞。  
  
5.  在 **[對應]** 資料表中，從空白資料列之 **[來源資料行]** 資料行的下拉式清單中選取來源資料行。 請確定來源資料行包含由兩個現有單一定義域所定址的複合定義域。 如果沒有對應的單一定義域存在，請按一下 **[建立定義域]** 圖示。  
  
6.  在 **[對應]** 資料表中，從空白資料列之 **[來源資料行]** 資料行的下拉式清單中選取來源資料行。 請確定來源資料行包含由兩個現有單一定義域所定址的複合定義域部分。 如果沒有對應的單一定義域存在，請按一下 **[建立定義域]** 圖示加以建立。 如需相關資訊，請參閱 [建立定義域](../data-quality-services/create-a-domain.md)。  
  
7.  按一下 **[建立複合定義域]** 圖示。  
  
##  <a name="DomainManagementActivity"></a> 在定義域管理活動中建立複合定義域  
  
1.  在 Data Quality Services 用戶端首頁中，按一下 **[開啟知識庫]** ，然後選取知識庫，或是按一下 **[新增知識庫]** ，並輸入新知識庫的屬性。  
  
2.  選取 **[定義域管理]** 當做活動，然後按一下 **[建立]** 建立新的知識庫，或按一下 **[開啟]** 開啟現有的知識庫。  
  
3.  確定複合定義域所需的兩個或多個單一定義域確實存在。 如果不存在，請按一下 **[建立定義域]** 圖示，並加以建立。 如需相關資訊，請參閱 [建立定義域](../data-quality-services/create-a-domain.md)。  
  
4.  在 **[定義域管理]** 頁面上，按一下定義域清單上方的 **[建立複合定義域]** 圖示。  
  
5.  輸入知識庫特有的名稱以及最多 256 個字元的描述。  
  
6.  在 **[定義域清單]** 中，選取將屬於複合定義域之一部分的定義域，並按一下向右箭號，將其移到 **[複合定義域中的定義域]** 資料表。  
  
7.  按一下 [確定] 。  
  
##  <a name="CompositeDomainProperties"></a> 設定複合定義域屬性  
  
1.  在 **[建立複合定義域]** 對話方塊中，輸入知識庫特有的名稱以及最多 256 個字元的描述。  
  
2.  在 **[定義域清單]** 中，選取將屬於複合定義域之一部分的定義域，並按一下向右箭號，將其移到 **[複合定義域中的定義域]** 資料表。 這是單一定義域的清單，您可將其加入至您所建立的複合定義域。 只有已經建立而且尚未加入至現有複合定義域的單一定義域才可使用。 單一定義域不能加入至知識庫內一個以上的複合定義域，而且複合定義域不能加入至另一個複合定義域。  
  
3.  按一下 **[進階]**。  
  
4.  針對 **[剖析方法]** 選取下列其中一項：  
  
    -   **參考資料**：根據參考資料服務 (RDS) 設定資料格式的方式來剖析欄位的值。 Data Quality Services 會將複合定義域中的值傳送給 RDS，而 RDS 會根據複合定義域中的定義域來傳回更正及剖析的資料。  
  
    -   **依照順序**：根據複合定義域中的定義域順序來剖析欄位的值。 第一個值將會併入第一個定義域，第二個值將會併入第二個定義域，依此類推。  
  
    -   **分隔符號**：根據選取 [分隔符號] 時從選項按鈕選取的分隔符號來剖析欄位的值。 這可以是 **[Tab 鍵]**、 **[分號]**、 **[逗號]**、 **[空格]** 或 **[其他]**。 如果是 **[其他]**，請輸入將會當做分隔符號的值。  
  
5.  如果您選取 **[分隔符號]** 當做剖析方法，您也可以選取 **[使用知識庫剖析]**。 如需詳細資訊，請參閱 [Knowledge-Based Parsing](#KnowledgeBaseParsing)。  
  
6.  按一下 **[完成]** ，完成定義域管理活動，如＜ [結束定義域管理活動](http://msdn.microsoft.com/library/ab6505ad-3090-453b-bb01-58435e7fa7c0)＞中所述。  
  
##  <a name="FollowUp"></a> 後續操作：建立複合定義域之後  
 在建立複合定義域之後，您可以針對定義域執行其他定義域管理工作、執行知識探索來將知識加入至定義域，或者將比對原則加入至定義域。 如需詳細資訊，請參閱[執行知識探索](../data-quality-services/perform-knowledge-discovery.md)、[管理定義域](../data-quality-services/managing-a-domain.md)或[建立比對原則](../data-quality-services/create-a-matching-policy.md)。  
  
##  <a name="KnowledgeBaseParsing"></a> Knowledge-Based Parsing  
 Data Quality Services 可讓您根據知識來剖析資料，而不只是根據分隔符號或順序。 當複雜來源資料對應至複合定義域，而且您並未使用參考資料服務時，將會使用以知識為基礎的剖析。 您可以使用以知識為基礎的剖析，將資料來源中的資料剖析成相關的單一定義域。 當使用以知識為基礎的剖析時，DQS 會先嘗試使用知識將複雜資料剖析成單一定義域。 如果可能的話，它會將字串的若干部分識別為在一個或多個定義域中，並將字串剖析為其各個定義域。 例如，假設您將 “John B. Doe” 當做完整名稱欄位中的複雜值，而該欄位是由「完整名稱」複合網域所表示。 如果 DQS 在「名字」網域中識別 “John”，在「姓氏」網域中識別 “Doe”， 則 DQS 會根據網域知識將 “B.” 加入「中間名」網域中。  
  
 只有當您同時選取以分隔符號為基礎的剖析時，才可以使用以知識為基礎的剖析。 以知識為基礎的剖析不會取代分隔符號剖析，而是會將它增強。 只有當沒有知識存在時，DQS 才會使用分隔符號執行剖析。 在某些情況下，DQS 可能會判斷某些剖析是根據以知識為基礎的剖析，並判斷其他剖析是根據以分隔符號為基礎的剖析。  
  
 當複合定義域是由字串定義域所組成，或者複合定義域是由混合不同類型的定義域 (整數、日期、時間等) 所組成時，便可以使用以知識為基礎的剖析。 如果資料來源是由不同類型的資料所組成，則應該先針對非字串資料類型來執行剖析，然後其餘資料則根據定義域知識，如上面所述。  
  
 當您使用以知識為基礎的剖析，而且來源資料中的值少於複合定義域中的定義域時，DQS 會在遺漏的定義域中放置 null。 當來源資料中的值多於複合定義域中的定義域時，DQS 會將額外的資料加入至其中一個資料行。 如果有兩個或多個定義域包含相同的值，則資料來源將會剖析為第一個相符的定義域。  
  
  
