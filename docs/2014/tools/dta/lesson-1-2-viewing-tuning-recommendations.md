---
title: 檢視微調建議 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Database Engine [SQL Server], tutorials
ms.assetid: e4e690c9-434f-4b01-b4de-0b905323ddd6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: fe8d52d898db35698155518646f074e7167687a0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66110183"
---
# <a name="viewing-tuning-recommendations"></a>檢視微調建議
  這項工作使用您先前在[微調工作負載](lesson-1-1-tuning-a-workload.md)中所建立的微調工作階段。 利用 MyScript.sql [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼微調好 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫之後，[!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor 會在 [建議]  索引標籤中顯示其結果。下列工作將介紹 [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor 圖形化使用者介面 (GUI) 的 [建議]  索引標籤，並引導您探索它針對微調工作階段結果所提供的相關資訊。  
  
### <a name="view-tuning-recommendations"></a>檢視微調建議  
  
1.  啟動 [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor。 請參閱 [啟動 Database Engine Tuning Advisor](../../relational-databases/performance/database-engine-tuning-advisor.md)。 請確定您連接[微調工作負載](lesson-1-1-tuning-a-workload.md)練習所用的相同 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。  
  
2.  在 [工作階段監視器]  窗格中，按兩下 [MySession]  。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor 會從先前的微調工作階段中載入工作階段資訊，而且會顯示 [建議]  索引標籤。請注意，[!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor 不會提供任何 [資料分割建議]  ，因為您接受所有微調選項預設值，而且在 [微調選項]  索引標籤中選取 [沒有資料分割]  。  
  
3.  在 [建議]  索引標籤上，利用索引標籤頁面底端的捲軸來檢視所有 [索引建議]  資料行。 每個資料列都代表一個 [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor 建議要卸除或建立的資料庫物件 (索引或索引檢視表)。 捲到最右側資料行，按一下 [定義]  。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor 會顯示一個 [SQL 指令碼預覽]  視窗，供您檢視在這個資料列上建立或卸除資料庫物件的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼。 按一下 [關閉]  來關閉預覽視窗。  
  
     如果您在尋找包含連結的 [定義]  時遇到困難，請按一下索引標籤式頁面底端的 [顯示現有的物件]  核取方塊加以清除，以減少顯示的資料列數。 當您清除這個核取方塊時，[!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor 只會顯示它已產生建議的物件。 選取 [顯示現有的物件]  核取方塊，以檢視 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫目前已存在的所有資料庫物件。 請利用索引標籤頁面右側的捲軸來檢視所有物件。  
  
4.  在 [索引建議]  窗格中，以滑鼠右鍵按一下方格。 這個右鍵功能表可讓您選取和取消選取各項建議。 您也可以利用它來變更方格文字的字型。  
  
5.  在 [動作]  功能表上，按一下 [儲存建議]  ，將所有建議儲存在單一 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼中。 指令碼命名`MySessionRecommendations.sql`。  
  
     在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 的查詢編輯器中，開啟 MySessionRecommendations.sql 指令碼來檢視它。 您可能會在查詢編輯器中執行這份指令碼，將建議套用在 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 範例資料庫上，但請勿執行這個動作。 請在查詢編輯器中關閉這份指令碼，不要執行它。  
  
     或者，您也可以在 [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor 的 [動作]  功能表上，按一下 [套用建議]  來套用建議，但現在請先不要在這個練習中套用這些建議。  
  
6.  如果 [建議]  索引標籤中存在多個建議，請清除某些在 [索引建議]  方格中列出資料庫物件的資料列。  
  
7.  在 **[動作]** 功能表上，按一下 **[評估建議]** 。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor 就會建立一個新的微調工作階段，供您評估 MySession 的部分原始建議。  
  
8.  型別`EvaluateMySession`新**工作階段名稱**，然後按一下**開始分析**工具列上的按鈕。 您可以針對這個新的微調工作階段，重複步驟 2 和 3 來檢視它的建議。  
  
## <a name="summary"></a>總結  
 您已檢視 MySession 微調工作階段的 [建議]  索引標籤內容，且已在新的 EvaluateMySession 微調工作階段中評估了它的部分建議。  
  
 如果您在執行工作階段之後，覺得必須變更微調選項，您可能需要評估部分微調建議。 例如，如果您要求 [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor 在指定工作階段的微調選項時考慮索引檢視表，但在產生建議之後，又決定不用索引檢視表。 此時，您可以利用 [動作]  功能表的 [評估建議]  選項，使 [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor 在不考慮索引檢視表的情況下，重新評估工作階段。 當您使用 [評估建議]  選項時，會以假設的方式，將先前產生的建議套用在目前的實體設計上，以達成第二個微調工作階段的實體設計。  
  
 您可以在 [報表]  索引標籤中，檢視其他微調結果資訊。這個課程的下一項工作會描述這個索引標籤。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [檢視微調報表](lesson-1-3-viewing-tuning-reports.md)  
  
  
