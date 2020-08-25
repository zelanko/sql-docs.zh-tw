---
title: 備份和還原資料庫
description: 遵循此教學課程，以了解如何使用 Azure Data Studio 備份及還原資料庫。
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: tutorial
author: markingmyname
ms.author: maghan
ms.reviewer: alayu, maghan, sstein
ms.custom: seodec18
ms.date: 11/04/2019
ms.openlocfilehash: 8594178dc6817cc8b826268c3fd0aebce59af2ec
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88765797"
---
# <a name="backup-and-restore-databases-using-azure-data-studio"></a>使用 Azure Data Studio 備份及還原資料庫

在本教學課程中，您將了解如何使用 Azure Data Studio 來執行下列動作：
> [!div class="checklist"]
> * 備份資料庫 
> * 檢視備份狀態
> * 產生用來執行備份的指令碼
> * 還原資料庫
> * 檢視還原工作的狀態

## <a name="prerequisites"></a>必要條件

本教學課程需要 SQL Server *TutorialDB*。 若要建立 *TutorialDB* 資料庫，請完成下列任一項快速入門：

* [使用 [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] 連線及查詢 SQL Server](quickstart-sql-server.md)

本教學課程需要連線到 SQL Server 資料庫。 Azure SQL Database 具有自動備份，因此 Azure Data Studio 不會執行 Azure SQL Database 備份及還原。 如需詳細資訊，請參閱 [Learn about automatic SQL Database backups](/azure/sql-database/sql-database-automated-backups) (了解自動 SQL Database 備份)。

## <a name="back-up-a-database"></a>備份資料庫

1. 開啟 TutorialDB 資料庫儀表板 (開啟 [伺服器] 提要欄位 (**CTRL+G**)，展開 [資料庫]，以滑鼠右鍵按一下 [TutorialDB]，然後選取 [管理])。

2. 開啟 [備份資料庫] 對話方塊 (按一下 [工作] 小工具中的 [備份])。

   ![[工作] 小工具](./media/tutorial-backup-restore-sql-server/tasks.png)

3. 本教學課程使用預設備份選項，因此請按一下 [備份]。
   ![[備份] 對話方塊](./media/tutorial-backup-restore-sql-server/backup-dialog.png)

按一下 [備份] 之後，[備份資料庫] 對話方塊即會消失，並開始備份程序。

## <a name="view-the-backup-status-and-view-the-backup-script"></a>檢視備份狀態和檢視備份指令碼

1. [工作歷程記錄] 窗格隨即出現，或按 **CTRL+T**。

   ![工作歷程](./media/tutorial-backup-restore-sql-server/task-history.png)

2. 若要在編輯器中檢視備份指令碼，請以滑鼠右鍵按一下 [Backup Database succeeded] \(已成功備份資料庫\)，然後選取 [指令碼]。

   ![備份指令碼](./media/tutorial-backup-restore-sql-server/task-script.png)

## <a name="restore-a-database-from-a-backup-file"></a>從備份檔案還原資料庫

1. 開啟 [伺服器] 提要欄位 (**CTRL+G**)，以滑鼠右鍵按一下您的伺服器，然後選取 [管理]。

2. 開啟 [還原資料庫] 對話方塊 (按一下 [工作] 小工具中的 [還原])。

   ![還原工作](media/tutorial-backup-restore-sql-server/tasks-restore.png)

3. 在 [還原來源] 欄位中選取 [備份檔案]。

4. 按一下 [備份檔案路徑] 欄位中的省略符號 (...)，然後選取 *TutorialDB* 的最新備份檔案。

5. 在 [目的地] 區段的 [目標資料庫] 欄位中鍵入 **TutorialDB_Restored**，將備份檔案還原到新的資料庫。 然後選取 [還原]。

   ![還原](./media/tutorial-backup-restore-sql-server/restore.png)

6. 若要檢視還原作業的狀態，請按 **CTRL+T** 開啟 [工作歷程記錄]。

   ![還原](./media/tutorial-backup-restore-sql-server/task-history-restore.png)