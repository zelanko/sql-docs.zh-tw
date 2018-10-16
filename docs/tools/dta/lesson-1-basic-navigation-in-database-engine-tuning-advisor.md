---
title: 課程 1：Database Engine Tuning Advisor 中的基本導覽 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Database Engine Tuning Advisor [SQL Server], tutorials
ms.assetid: ad49b2e0-a5e3-49d2-80fd-9f4eaa3652cb
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ee0b1c221c3bdb18ec9b79339e9dd55cb4eed93e
ms.sourcegitcommit: 5d6e1c827752c3aa2d02c4c7653aefb2736fffc3
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/10/2018
ms.locfileid: "49071802"
---
# <a name="lesson-1-basic-navigation-in-database-engine-tuning-advisor"></a>第 1 課：Database Engine Tuning Advisor 中的基本導覽
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
Database Engine Tuning Advisor 提供一種以圖形化使用者介面 (GUI) 為基礎的方法，供您檢視微調工作階段和微調建議報表。 這個課程將為您示範如何啟動這個工具，以及如何設定顯示畫面。 在這個課程結束時，您會知道多種啟動工具的方法，以及如何設定它的顯示畫面來支援您定期執行的微調工作。  

## <a name="prerequisites"></a>Prerequisites 

若要完成本教學課程，您需要 SQL Server Management Studio、執行 SQL Server 伺服器的存取權，以及 AdventureWorks 資料庫。

- 安裝 [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。
- 安裝 [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads)。
- 下載 [AdventureWorks2017 範例資料庫](https://docs.microsoft.com/sql/samples/adventureworks-install-configure?view=sql-server-2017) \(機器翻譯\)。


如需在 SSMS 中還原資料庫的指示，請參閱：[還原資料庫](https://docs.microsoft.com/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms?view=sql-server-2017)。

  >[!NOTE]
  > 本教學課程適用於使用者熟悉如何使用 SQL Server Management Studio 和基本資料庫管理工作。 
  

## <a name="launch-database-tuning-advisor"></a>啟動 Database Tuning Advisor 
首先，請開啟 Database Engine Tuning Advisor (DTA) 圖形化使用者介面 (GUI)。 在第一次使用時， **系統管理員** 固定伺服器角色的成員必須啟動 Database Engine Tuning Advisor 來初始化應用程式。 初始化之後， **db_owner** 固定資料庫角色的成員便可以利用 Database Engine Tuning Advisor 來微調他們擁有的資料庫。 如需初始化 Database Engine Tuning Advisor 的詳細資訊，請參閱 [啟動及使用 Database Engine Tuning Advisor](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)。  
  
1. 啟動 SQL Server Management Studio (SSMS)。 在 Windows 上 **[開始] 功能表**，指向**所有程式**並找出**SQL Server Management Studio**。 
2. 一旦開啟 SSMS，請選取**工具**功能表，然後選取**Database Tuning Advisor**。 

  ![啟動 SSMS 從 DTA](media/dta-tutorials/launch-dta.png)

3. Database Tuning Advisor 會自行啟動，並開啟**連接到伺服器** 對話方塊。 確認預設設定，然後按**Connect**連接到您的 SQL Server。  
  
依預設，Database Engine Tuning Advisor 會開啟下列說明中的組態：  
  
![Database Engine Tuning Advisor 預設視窗](media/dta-tutorials/dta-default-gui.png)
  
> [!NOTE]  
> **工作階段監視器**索引標籤會顯示工作階段名稱，這是目前的資料與已連線的使用者名稱。 
  
在第一次開啟 Database Engine Tuning Advisor 時，它的 GUI 會出現兩個主要窗格。  
  
-   左窗格包含「工作階段監視器」，它會列出這個 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體已執行的所有微調工作階段。 當您開啟 Database Engine Tuning Advisor 時，它會在窗格頂端顯示一個新的工作階段。 您可以在相鄰的窗格中命名這個工作階段。 一開始，只列出預設工作階段。 這是 Database Engine Tuning Advisor 自動建立的預設工作階段。 微調資料庫之後，您連接的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的所有微調工作階段都會列在這個新的工作階段之下。 您可以以滑鼠右鍵按一下微調工作階段，對它進行重新命名、調整、刪除或複製等動作。 如果您在清單中按一下滑鼠右鍵，您可以依名稱、狀態或建立時間來排序工作階段，也可以建立新的工作階段。 這個窗格的底端區段會顯示所選微調工作階段的詳細資料。 您可以選擇使用 [分類] 按鈕將詳細資料組成類別目錄，來顯示詳細資料，也可以使用 [字母順序] 按鈕，以字母順序清單顯示它們。 您也可以將右窗格框線拖曳至視窗左邊來隱藏工作階段監視器。 若要重新檢視它，將窗格框線拖回至右邊即可。 您可以利用工作階段監視器來檢視先前的微調工作階段，也可以利用它們來建立含有類似定義的新工作階段。 您也可以利用工作階段監視器來評估微調建議。 如需詳細資訊，請參閱[檢視及處理 Database Engine Tuning Advisor 的輸出](../../relational-databases/performance/view-and-work-with-the-output-from-the-database-engine-tuning-advisor.md)。 請利用瀏覽器中的 [上一頁] 按鈕來返回這個教學課程。  
  
-   右窗格包含 [一般] 和 [微調選項] 索引標籤。 您可以在這裡定義您的 Database Engine 微調工作階段。 在 [一般] 索引標籤中，輸入微調工作階段的名稱，指定要使用的工作負載檔案或資料表，並選取您要在此工作階段中進行微調的資料庫和資料表。 工作負載是針對需要微調的一或多個資料庫來執行的一組 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。 當微調資料庫時，Database Engine Tuning Advisor 會利用追蹤檔、追蹤資料表、[!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼或 XML 檔來作為工作負載輸入。 您可以在 [微調選項] 索引標籤中，選取實體資料庫設計結構 (索引或索引檢視)，以及在分析期間，Database Engine Tuning Advisor 所要考量的資料分割策略。 在這個索引標籤中，您也可以指定 Database Engine Tuning Advisor 微調工作負載所花的最大時間。 依預設，Database Engine Tuning Advisor 會微調工作負載一小時。  
  
> [!NOTE]  
> 當從 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查詢編輯器匯入 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 指令碼時，Database Engine Tuning Advisor 可以採用 XML 檔來作為輸入。 如需詳細資訊，請參閱 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 啟動及使用 Database Engine Tuning Advisor [中有關從](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)查詢編輯器＜啟動 Database Engine Tuning Advisor＞一節。  
  
## <a name="configure-tool-options-and-layout"></a>設定工具選項和配置 

1.  在 **[工具]** 功能表上，按一下 **[選項]**。  

   ![DTA 選項](media/dta-tutorials/dta-settings.png) 
  
2.  在 [選項] 對話方塊中，檢視下列選項：  
  
    -   展開 [啟動時] 清單來檢視 Database Engine Tuning Advisor 啟動時所能顯示的項目。 依預設，會選取 [顯示新的工作階段]。  
  
    -   按一下 [變更字型]，了解您在 [一般] 索引標籤上可以為資料庫和資料表清單選擇哪些字型。執行微調之後，Database Engine Tuning Advisor 的建議方格和報表也會使用這個選項所選擇的字型。 依預設，Database Engine Tuning Advisor 會使用系統字型。  
  
    -   [最近使用清單中的項目數目] 的設定範圍在 **1** 和 **10** 之間。 請在 [檔案] 功能表上，按一下 [最近使用的工作階段] 或 [最近使用的檔案] 來設定所顯示清單中的最大項目數。 依預設，這個選項會設為 **4**。  
  
    -   當核取 [記住上次的微調選項] 時，依預設，Database Engine Tuning Advisor 會利用上一個微調工作階段所指定的微調選項來處理下一個微調工作階段。 請清除這個核取方塊來使用 Database Engine Tuning Advisor 微調選項預設值。 依預設，會選取這個選項。  
  
    -   依預設，會核取 [永久刪除工作階段之前先詢問] 來避免意外刪除微調工作階段。  
  
    -   依預設，會核取 [停止工作階段分析之前先詢問]，以避免在 Database Engine Tuning Advisor 分析工作負載完成之前不慎停止微調工作階段。  
  
## <a name="next-lesson"></a>下一課  
[課程 2：使用 Database Engine Tuning Advisor](../../tools/dta/lesson-2-using-database-engine-tuning-advisor.md)  
  
  
  
