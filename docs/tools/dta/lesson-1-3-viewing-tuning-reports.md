---
title: "檢視微調報表 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-query-tuning
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
helpviewer_keywords: tuning reports [SQL Server]
ms.assetid: daee6143-269f-428b-8458-9a3e726d586c
caps.latest.revision: "21"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1a3fca4cfcb035c48e37c455e72b03a76474a3cd
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="lesson-1-3---viewing-tuning-reports"></a>課程 1-3-檢視微調報表
在這個課程的上一個練習中，您檢視了在 MySession 微調工作階段所產生的 Database Engine Tuning Advisor 建議中建立或卸除資料庫物件的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼。 MySession 微調工作階段是先前在 [微調工作負載](../../tools/dta/lesson-1-1-tuning-a-workload.md)中所建立的。  
  
雖然檢視用來實作微調結果的指令碼非常有用，但 Database Engine Tuning Advisor 也另外提供了許多有用的報表，供您檢視。 這些報表提供您在微調的資料庫其中之現有實體設計結構的相關資訊，以及所建議之結構的相關資訊。 您可以依照下列練習中的說明，按一下 [報表] 索引標籤來檢視這些微調報表。 這個練習使用[微調工作負載](../../tools/dta/lesson-1-1-tuning-a-workload.md)和[檢視微調建議](../../tools/dta/lesson-1-2-viewing-tuning-recommendations.md)中所建立的 MySession 和 EvaluateMySession 微調工作階段。  
  
### <a name="view-tuning-reports"></a>檢視微調報表  
  
1.  啟動 Database Engine Tuning Advisor。 請參閱 [啟動 Database Engine Tuning Advisor](../../tools/dta/lesson-1-1-launching-database-engine-tuning-advisor.md)。 請確定您連接了這個課程先前之練習所用的相同 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。  
  
    在 [工作階段監視器] 窗格中，按兩下 [MySession]。 Database Engine Tuning Advisor 會從這個工作階段中，載入工作階段資訊。  
  
2.  按一下 [報表] 索引標籤。  
  
3.  在 [微調摘要] 窗格中，您可以檢視這個微調工作階段的相關資訊。 請利用捲軸來檢視所有窗格內容。 請注意 [預期的改進百分比] 和 [建議使用的空間]。 當您設定微調選項時，可能會限制建議所用的空間。 在 [微調選項] 索引標籤上，選取 [進階選項]。 核取 [定義建議的最大空間]，並指定建議組態可使用的最大空間 (以 MB 表示)。 請利用說明瀏覽器中的 [上一頁] 按鈕來返回這個教學課程。  
  
4.  在 [微調報表] 窗格中，按一下 [選取報表] 清單中的 [陳述式成本報表]。 如果您需要更多空間來檢視報表，請向左拖曳 [工作階段監視器] 窗格框線。 每個針對資料庫中某份資料表來執行的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式都有相關的效能成本。 您可以在資料表中常常存取的資料行上建立有效的索引來降低這個效能成本。 這份報表會顯示執行工作負載中某陳述式的原始成本和實作微調建議的成本之間的估計改進百分比。 請注意，報表所包含的資訊量以工作負載的長度和複雜度為基礎。  
  
5.  以滑鼠右鍵按一下方格區域中的 [陳述式成本報表] 窗格，然後按一下 [匯出至檔案]。 將報表儲存成 **MyReport**。 檔案名稱會自動附加 .xml 副檔名。 您可以在喜愛的 XML 編輯器或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，開啟 MyReport.xml 來檢視報表內容。  
  
6.  返回 Database Engine Tuning Advisor 的 [報表] 索引標籤，然後以滑鼠右鍵按一下 [陳述式成本報表]。 檢視其他可用的選項。 請注意，您可以變更所檢視之報表的字型。 在這裡變更字型，也會變更其他索引標籤頁面的字型。  
  
7.  在 [選取報表] 清單中，按一下其他報表來熟悉它們。  
  
## <a name="summary"></a>摘要  
現在，您已在 Database Engine Tuning Advisor GUI 的 [報表] 索引標籤中，探索了 MySession 微調工作階段。 您可以利用這些相同的步驟來探索針對 EvaluateMySession 微調工作階段而產生的報表。 請在 [工作階段監視器] 窗格中，按兩下 [EvaluateMySession] 來開始作業。  
  
## <a name="next-lesson"></a>下一課  
[第 3 課：使用 dta 命令提示字元公用程式](../../tools/dta/lesson-3-using-the-dta-command-prompt-utility.md)  
  
  
  
