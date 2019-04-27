---
title: 建立連結的定義域 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql12.dqs.kb.linkeddomain.f1
ms.assetid: fd99d422-c53d-4d7c-9cdd-303c703683b6
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 800326d3255180087cb7603435e2d0e1a8c8e029
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62755727"
---
# <a name="create-a-linked-domain"></a>建立連結的定義域
  此主題描述如何在 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 中的知識庫內建立連結的定義域。 連結的定義域是從另一個定義域 (之前已經存在的定義域) 建立而來，而且會從它連結的定義域繼承所有值、規則和屬性，除了名稱和描述以外。 您可以將一組連結的定義域當做一個定義域來管理。 藉由連結一個定義域與另一個定義域，您所建立的定義域就會從另一個定義域繼承其內容。  
  
## <a name="scenarios"></a>案例  
 連結的定義域在以下情況下特別有用。  
  
### <a name="mapping-multiple-fields-to-domains-that-share-values-rules-and-properties"></a>將多個欄位對應到共用值、規則和屬性的定義域  
 您不能將兩個欄位對應到相同定義域，但是可以將一個欄位對應到定義域，然後將第二個欄位對應到與第一個定義域連結的定義域。 這樣做會將欄位對應到擁有相同內容和屬性 (名稱和描述除外) 的兩個不同定義域。 如需詳細資訊，請參閱 [Map two fields to linked domains](#Map)。  
  
### <a name="controlling-data-flow-to-composite-domains"></a>控制與複合定義域之間的資料流程  
 連結的定義域可讓您控制欄位與複合定義域之間的資料流程。 當某個欄位的資料流向複合定義域中，以及另一個非常類似的欄位中的資料未流向此複合定義域時，您可以加以區分。 當您要這樣做時，您會指定在兩個連結的定義域中，一個定義域是複合定義域的一部分，另一個定義域則否。 從定義域的觀點來看，連結的定義域是相同的。 它們包含相同的知識。 但是從複合定義域的觀點來看，連結的定義域是不同的。 其中一個會參與複合定義域，另一個則否。  
  
 範例是包含下列欄位的記錄：客戶名字、客戶姓氏和父親的名字。 假設您將客戶名字和父親的名字對應到「名字」定義域，並讓「名字」定義域和「姓氏」定義域成為「完整名稱」複合定義域的一部分。 問題是父親的名字將會加入至複合定義域，而且不含姓氏。 但是，如果您將兩個名字欄位中的每一個都連結到定義域，並連結這兩個定義域，然後您可以將「客戶名字」定義域加入至「完整名稱」複合定義域，而不將「父親的名字」欄位加入至複合定義域，以免「父親的名字」被加入至複合定義域。  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Prerequisites"></a> 必要條件  
 若要建立連結的定義域，您必須擁有知識庫以及您想要連結的現有定義域。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
 您必須擁有 DQS_MAIN 資料庫的 dqs_kb_editor 角色或 dqs_administrator 角色，才能建立連結的定義域。  
  
##  <a name="Create"></a> 建立連結的定義域  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [執行 Data Quality Client 應用程式](../../2014/data-quality-services/run-the-data-quality-client-application.md)。  
  
2.  在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 首頁畫面上，開啟或建立知識庫。 選取 **[定義域管理]** 當做活動，然後按一下 **[開啟]** 或 **[建立]**。 如需相關資訊，請參閱 [建立知識庫](../../2014/data-quality-services/create-a-knowledge-base.md) 或 [開啟知識庫](../../2014/data-quality-services/open-a-knowledge-base.md)。  
  
3.  從 **[定義域管理]** 頁面的 **[定義域清單]** 中，以滑鼠右鍵按一下您想要與新的定義域連結的定義域，然後按一下 **[建立連結的定義域]**。  
  
    > [!NOTE]  
    >  並沒有專門用來建立連結的定義域的圖示。 若要這樣做，您只能使用內容功能表中的命令。  
  
4.  在 **[建立定義域]** 對話方塊中，輸入知識庫特有的名稱以及最多 256 個字元的描述。 確認連結到的定義域名稱正確無誤。  
  
5.  按一下 **[確定]** ，完成建立連結的定義域。  
  
6.  必要時，您可以在 [定義域屬性] 索引標籤中變更連結的定義域的名稱或描述。  
  
7.  按一下 **[完成]** ，完成定義域管理活動，如＜ [結束定義域管理活動](../../2014/data-quality-services/end-the-domain-management-activity.md)＞中所述。  
  
##  <a name="Map"></a> Map two fields to linked domains  
  
1.  開啟知識探索活動中的知識庫，並將知識庫對應到資料庫及資料表或檢視表。  
  
2.  將一個欄位對應到定義域，然後嘗試將第二個欄位對應的相同的定義域。  
  
3.  如果快顯視窗指出此定義域已在使用中，請按一下 [是] 建立連結的定義域。  
  
4.  在 [建立定義域] 對話方塊中，輸入定義域名稱和描述，然後按一下 [確定]。  
  
##  <a name="FollowUp"></a> 後續操作：建立連結的定義域之後  
 在建立連結的定義域之後，您可以針對定義域執行其他定義域管理工作、執行知識探索來將知識加入至定義域，或者將比對原則加入至定義域。 如需詳細資訊，請參閱[執行知識探索](../../2014/data-quality-services/perform-knowledge-discovery.md)、[管理定義域](../../2014/data-quality-services/managing-a-domain.md)或[建立比對原則](../../2014/data-quality-services/create-a-matching-policy.md)。  
  
##  <a name="Behavior"></a> 連結的定義域行為  
 您可以為連結的定義域變更設定，如下所示：  
  
-   您可以變更連結的定義域的名稱和描述。  
  
-   若要針對 **[資料類型]**、 **[使用前置值]** 或 **[設定輸出格式為]** 屬性變更定義域屬性，請選取您連結到的定義域，並在 **[定義域屬性]** 索引標籤中針對該定義域變更這些設定。 您不能在連結的定義域的屬性中變更這些設定。 如需相關資訊，請參閱 [建立定義域](../../2014/data-quality-services/create-a-domain.md)。  
  
-   [定義域管理] 頁面上 **[參考資料]**、 **[定義域規則]**、 **[定義域值]** 和 **[以詞彙為主的關聯]** 索引標籤中的設定可以針對連結的定義域或是連結到的定義域來變更，而且另一個定義域將會繼承變更。  
  
 連結的定義域具有下列特性：  
  
-   您不能取消連結兩個定義域。 若要移除連結，請刪除其中一個連結的定義域。  
  
-   當您在 [定義域管理] 頁面上的定義域清單中選取連結的定義域時，於包含 **[值]** 資料表的窗格中識別連結的定義域的字串會包含指示，指出此定義域是連結的定義域。  
  
-   如果您刪除另一個定義域所連結到的定義域，將會一併刪除兩個定義域。 但是，您可以刪除連結的定義域，而且將不會刪除連結到的定義域。  
  
-   連結的定義域不能連結到本身與另一個定義域連結的定義域。  
  
-   您不能建立與複合定義域之間的連結的定義域或連結的複合定義域。  
  
-   當您在任何 [定義域管理] 索引標籤中按兩下連結的定義域時，將會開啟此定義域進行編輯，而且在名稱字串中會指示它是連結的定義域。  
  
  
