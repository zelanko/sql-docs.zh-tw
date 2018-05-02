---
title: 啟動 dta 命令提示字元公用程式和微調工作負載 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: dta
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-query-tuning
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- Database Engine [SQL Server], tutorials
ms.assetid: f34a5acf-1f3b-4484-a770-6470cb925ab0
caps.latest.revision: 28
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b4adf756444c22146108fead4f607c20c6108dc3
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/17/2018
---
# <a name="lesson-3-1---starting-the-dta-command-prompt-utility-and-tuning-a-workload"></a>課程 3-1 - 啟動 dta 命令提示字元公用程式和調整工作負載
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 這項工作會帶您逐步啟動 **dta** 公用程式、檢視它的說明，再從命令提示字元之下，使用它來微調工作負載。 它會使用您在 Database Engine Tuning Advisor 圖形化使用者介面 (GUI) 的 [微調工作負載](../../tools/dta/lesson-1-1-tuning-a-workload.md)練習中所建立的 MyScript.sql 工作負載。  
  
本教學課程使用 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 範例資料庫。 基於安全性的考量，依預設，不會安裝範例資料庫。 若要安裝範例資料庫，請參閱＜ [安裝 SQL Server 範例和範例資料庫](http://sqlserversamples.codeplex.com)＞。  
  
下列工作將帶您逐步開啟命令提示字元、啟動 **dta** 命令提示字元公用程式、檢視其語法說明，以及微調您在 [微調工作負載](../../tools/dta/lesson-1-1-tuning-a-workload.md)中所建立的簡單工作負載 MyScript.sql。  
  
### <a name="to-start-the-dta-command-prompt-utility-and-view-help"></a>若要啟動 dta 命令提示字元公用程式和檢視說明  
  
1.  在 [開始] 功能表上，依序指向 [所有程式] 和 [附屬應用程式]，再按一下 [命令提示字元]。  
  
2.  在命令提示字元之下，輸入下列字串，再按 ENTER 鍵：  
  
    ```  
    dta -? | more  
    ```  
  
    這個命令的 `| more` 部份是選擇性的。 不過，您可以利用它來逐頁閱讀公用程式的語法說明。 按 ENTER 鍵會在說明文字中，每次前進一行，按空白鍵則會每次前進一頁。  
  
### <a name="to-tune-a-simple-workload-by-using-the-dta-command-prompt-utility"></a>若要利用 dta 命令提示字元公用程式來微調簡單的工作負載  
  
1.  在命令提示字元之下，導覽到儲存 MyScript.sql 檔的目錄。  
  
2.  在命令提示字元之下，輸入下列字串，再按 ENTER 鍵來執行命令，以及啟動微調工作階段 (請注意，當剖析命令時，這個公用程式會區分大小寫)：  
  
    ```  
    dta -S YourServerName\YourSQLServerInstanceName -E -D AdventureWorks2012 -if MyScript.sql -s MySession2 -of MySession2OutputScript.sql -ox MySession2Output.xml -fa IDX_IV -fp NONE -fk NONE  
    ```  
  
    其中 `-S` 指定您的伺服器名稱以及安裝了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫的 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 執行個體。 `-E` 設定值指定您要使用執行個體的信任連接，當您利用 Windows 網域帳戶來連接時，適合採用這個方式。 `-D` 設定值指定您要微調的資料庫， `-if` 指定工作負載檔案， `-s` 指定工作階段名稱， `-of` 指定工具要將 [!INCLUDE[tsql](../../includes/tsql-md.md)] 建議指令碼寫入其中的檔案， `-ox` 指定工具要將 XML 格式的建議寫入其中的檔案。 最後三個參數依照下列方式來指定微調選項： `-fa IDX_IV` 指定 Database Engine Tuning Advisor 只應考慮加入索引 (叢集和非叢集) 和索引檢視； `-fp NONE` 指定在分析期間，完全不應考慮任何資料分割策略； `-fk NONE` 指定 Database Engine Tuning Advisor 在產生建議時，不需要保留資料庫中任何現有的實體設計結構。  
  
3.  在 Database Engine Tuning Advisor 微調好工作負載之後，它會顯示一則訊息，指出微調工作階段已順利完成。 您可以利用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 來開啟 MySession2OutputScript.sql 和 MySession2Output.xml 檔，以檢視微調結果。 另外，您也可以在 Database Engine Tuning Advisor GUI 中開啟 MySession2 微調工作階段，依照 [檢視微調建議](../../tools/dta/lesson-1-2-viewing-tuning-recommendations.md) 和 [檢視微調報表](../../tools/dta/lesson-1-3-viewing-tuning-reports.md)中的相同方式來檢視其建議和報表。  
  
## <a name="summary"></a>摘要  
您已在命令提示字元之下，利用 **dta** 公用程式完成了簡單工作負載的微調。 這個工具也提供了許多其他微調選項。 如需詳細資訊，請參閱工具說明 (**dta -?**) 和參考主題 [dta 公用程式](../../tools/dta/dta-utility.md) 。  
  
## <a name="after-you-finish-this-tutorial"></a>完成這個教學課程之後  
完成這個教學課程中的課程之後，請參閱下列主題，以取得有關 Database Engine Tuning Advisor 的詳細資訊：  
  
-   ＜[Database Engine Tuning Advisor](../../relational-databases/performance/database-engine-tuning-advisor.md) ＞提供如何利用這個工具來執行工作的描述。  
  
-   ＜[dta Utility](../../tools/dta/dta-utility.md) ＞提供有關命令提示字元公用程式的參考資料，以及可用來控制公用程式作業的選擇性 XML 檔案。  
  
若要返回教學課程的開頭，請參閱 [教學課程：Database Engine Tuning Advisor](../../tools/dta/tutorial-database-engine-tuning-advisor.md)。  
  
## <a name="see-also"></a>另請參閱  
[Database Engine 教學課程](../../relational-databases/database-engine-tutorials.md)  
  
  
  
