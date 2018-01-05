---
title: "備份和還原資料庫，使用 SQL 作業 Studio （預覽） |Microsoft 文件"
description: "了解如何備份和還原資料庫，使用 SQL 作業 Studio （預覽）"
ms.custom: tools|sos
ms.date: 11/15/2017
ms.prod: sql-non-specified
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: 
ms.topic: tutorial
author: erickangMSFT
ms.author: erickang
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 46ef55aa54275e356eff9674aac10a27b36d758e
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="backup-and-restore-using-includename-sosincludesname-sos-shortmd"></a>備份及還原使用[!INCLUDE[name-sos](../includes/name-sos-short.md)]

您可以在本教學課程，了解如何使用[!INCLUDE[name-sos](../includes/name-sos-short.md)]至：
> [!div class="checklist"]
> * 備份資料庫 
> * 檢視備份狀態
> * 產生用來執行備份的指令碼
> * 還原資料庫
> * 檢視的還原工作的狀態

## <a name="prerequisites"></a>Prerequisites

本教學課程需要 SQL Server *TutorialDB*。 若要建立*TutorialDB*資料庫，請完成下列快速入門的其中一個：

- [連接及查詢 SQL Server 使用[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-server.md)


## <a name="backup-a-database"></a>備份資料庫

1. 開啟 TutorialDB 資料庫儀表板 (開啟**伺服器**[資訊看板] (**CTRL + G**)，依序展開**資料庫**，以滑鼠右鍵按一下**TutorialDB**，選取**管理**)。 

2. 開啟**Backup database**對話方塊 (按一下**備份**上**工作**widget)。

   ![工作小工具](./media/tutorial-backup-restore-sql-server/tasks.png)

3. 本教學課程使用的預設備份選項，所以按**備份**。
   ![備份對話方塊](./media/tutorial-backup-restore-sql-server/backup-dialog.png)

按一下後**備份**、 **Backup database**對話方塊消失，開始備份程序。

## <a name="view-the-backup-status-and-view-the-backup-script"></a>檢視備份狀態，並檢視備份指令碼

1. 開啟**工作歷程記錄**[資訊看板] 上按一下 [時鐘] 圖示*動作列*或按**CTRL + T**。

   ![工作歷程記錄](./media/tutorial-backup-restore-sql-server/task-history.png)

2. 若要檢視備份指令碼編輯器中，以滑鼠右鍵按一下**成功的備份資料庫**選取**指令碼**。

   ![備份指令碼](./media/tutorial-backup-restore-sql-server/task-script.png) 

## <a name="restore-a-database-from-a-backup-file"></a>將資料庫從備份檔案還原


1. 開啟**伺服器**[資訊看板] (**CTRL + G**)，以滑鼠右鍵按一下您的伺服器，然後選取**管理**。 

2. 開啟**還原資料庫**對話方塊 (按一下**還原**上**工作**widget)。

2. 選取**備份檔案**中**從還原**欄位。 

3. 按一下省略符號 （...） 在**備份檔案路徑**欄位，並選取最新的備份檔案*TutorialDB*。

3. 型別**TutorialDB_Restored**中**目標資料庫**欄位**目的地**區段，以將備份檔案還原到新的資料庫。

   ![還原](./media/tutorial-backup-restore-sql-server/restore.png)

4. 按一下**還原**

5. 若要檢視還原作業的狀態，請按一下**CTRL + T**開啟**工作歷程記錄**[資訊看板]。

   ![還原](./media/tutorial-backup-restore-sql-server/task-history-restore.png)


在此教學課程中，您學會如何：
> [!div class="checklist"]
> * 備份資料庫 
> * 檢視備份狀態
> * 產生用來執行備份的指令碼
> * 還原資料庫
> * 檢視的還原工作的狀態

