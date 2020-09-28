---
title: 備份和還原資料庫
description: 依照本教學課程的指示，了解如何使用 Azure Data Studio 備份及還原資料庫。
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: tutorial
author: markingmyname
ms.author: maghan
ms.reviewer: alayu
ms.custom: seodec18
ms.date: 11/04/2019
ms.openlocfilehash: 808dec10c92bffe66122bfa9a55d7db1cc64f62e
ms.sourcegitcommit: 63aef5a96905f0b026322abc9ccb862ee497eebe
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/25/2020
ms.locfileid: "91364168"
---
# <a name="tutorial-back-up-and-restore-databases-using-azure-data-studio"></a>教學課程：使用 Azure Data Studio 備份及還原資料庫

在本教學課程中，您將了解如何使用 Azure Data Studio 來執行下列動作：
> [!div class="checklist"]
> * 備份資料庫。
> * 檢視備份狀態。
> * 產生用來執行備份的指令碼。
> * 還原資料庫。
> * 檢視還原工作的狀態。

## <a name="prerequisites"></a>必要條件

本教學課程需要 SQL Server *TutorialDB*。 若要建立 TutorialDB 資料庫，請完成下列快速入門：

* [使用 Azure Data Studio 連線及查詢 SQL Server](quickstart-sql-server.md)

本教學課程需要連線至 SQL Server 資料庫。 Azure SQL Database 具有自動備份，因此 Azure Data Studio 不會執行 Azure SQL Database 備份及還原。 如需詳細資訊，請參閱[了解自動 SQL Database 備份](/azure/sql-database/sql-database-automated-backups)。

## <a name="back-up-a-database"></a>備份資料庫

1. 開啟 [伺服器] 提要欄位，以開啟 TutorialDB 資料庫儀表板。 然後，選取 **Ctrl+G**，展開 [資料庫]，以滑鼠右鍵按一下 **TutorialDB**，然後選取 [管理]。

1. 在 [工作] widget 上選取 [備份]，以開啟 [備份資料庫] 對話方塊。

   ![顯示工作 widget 的螢幕擷取畫面。](./media/tutorial-backup-restore-sql-server/tasks.png)

1. 本教學課程使用預設備份選項，因此請選取 [備份]。

   ![顯示 [備份] 對話方塊的螢幕擷取畫面。](./media/tutorial-backup-restore-sql-server/backup-dialog.png)

選取 [備份] 之後，[備份資料庫] 對話方塊即會消失，並開始進行備份程序。

## <a name="view-the-backup-status-and-the-backup-script"></a>檢視備份狀態和備份指令碼

1. [工作歷程記錄] 窗格隨即出現，或選取 **CTRL+T** 加以開啟。

   ![顯示 [工作歷程記錄] 窗格的螢幕擷取畫面。](./media/tutorial-backup-restore-sql-server/task-history.png)

1. 若要在編輯器中檢視備份指令碼，請以滑鼠右鍵按一下 [Backup Database succeeded] \(已成功備份資料庫\)，然後選取 [指令碼]。

   ![顯示備份指令碼的螢幕擷取畫面。](./media/tutorial-backup-restore-sql-server/task-script.png)

## <a name="restore-a-database-from-a-backup-file"></a>從備份檔案還原資料庫

1. 選取 **Ctrl+G** 以開啟 [伺服器] 提要欄位。 然後，以滑鼠右鍵按一下您的伺服器，並選取 [管理]。

1. 在 [工作] widget 上選取 [還原]，以開啟 [還原資料庫] 對話方塊。

   ![顯示工作還原的螢幕擷取畫面。](media/tutorial-backup-restore-sql-server/tasks-restore.png)

1. 在 [還原來源] 方塊中選取 [備份檔案]。

1. 選取 [備份檔案路徑] 方塊中的省略符號 (...)，然後選取 *TutorialDB* 的最新備份檔案。

1. 在 [目的地] 區段的 [目標資料庫] 方塊中輸入 **TutorialDB_Restored**，將備份檔案還原到新的資料庫。 然後選取 [還原]。

   ![顯示還原備份的螢幕擷取畫面。](./media/tutorial-backup-restore-sql-server/restore.png)

1. 若要檢視還原作業的狀態，請選取 **Ctrl+T** 以開啟 [工作歷程記錄]。

   ![顯示歷程記錄工作還原的螢幕擷取畫面。](./media/tutorial-backup-restore-sql-server/task-history-restore.png)