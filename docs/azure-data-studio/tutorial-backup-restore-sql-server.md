---
title: 備份和還原資料庫，使用 Azure Data Studio |Microsoft Docs
description: 了解如何備份和還原資料庫，使用 Azure Data Studio
ms.custom: tools|sos
ms.date: 09/24/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: tutorial
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f2d9b4cbee5ab4da44961927809bf1fb4c771cc1
ms.sourcegitcommit: 35e4c71bfbf2c330a9688f95de784ce9ca5d7547
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/16/2018
ms.locfileid: "49355909"
---
# <a name="backup-and-restore-using-includename-sosincludesname-sos-shortmd"></a>使用[!INCLUDE[name-sos](../includes/name-sos-short.md)]備份及還原

您可以在本教學課程，了解如何使用[!INCLUDE[name-sos](../includes/name-sos-short.md)]:
> [!div class="checklist"]
> * 備份資料庫 
> * 檢視備份狀態
> * 產生用來執行備份的指令碼
> * 還原資料庫
> * 檢視還原工作的狀態

## <a name="prerequisites"></a>必要條件

本教學課程需要 SQL Server *TutorialDB*。 若要建立*TutorialDB*資料庫，請完成下列其中一項快速入門教學：

- [使用 [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] 連接及查詢 SQL Server](quickstart-sql-server.md)


## <a name="backup-a-database"></a>備份資料庫

1. 開啟 TutorialDB 資料庫儀表板 (開啟**伺服器**[資訊看板] (**CTRL + G**)，展開**資料庫**，以滑鼠右鍵點選 **TutorialDB** ，選取**管理**)。 

2. 開啟**Backup database**  對話方塊 (按一下**備份**上**工作**小工具)。

   ![工作小工具](./media/tutorial-backup-restore-sql-server/tasks.png)

3. 本教學課程使用預設的備份選項，所以按一下**備份**。
   ![備份對話方塊](./media/tutorial-backup-restore-sql-server/backup-dialog.png)

按一下**備份**後，**Backup database** 對話方塊消失並開始備份程序。

## <a name="view-the-backup-status-and-view-the-backup-script"></a>檢視備份狀態與檢視備份指令碼

1. 開啟**工作歷程記錄**資訊看板 上按一下時鐘圖示*動作列*或按下**CTRL + T**。

   ![工作歷程記錄](./media/tutorial-backup-restore-sql-server/task-history.png)

2. 若要檢視備份的指令碼編輯器中，以滑鼠右鍵按一下**成功備份的資料庫**，然後選取**指令碼**。

   ![備份指令碼](./media/tutorial-backup-restore-sql-server/task-script.png) 

## <a name="restore-a-database-from-a-backup-file"></a>從備份檔案還原資料庫


1. 開啟**伺服器**資訊看板 (**CTRL + G**)，以滑鼠右鍵按一下您的伺服器，然後選取**管理**。 

2. 開啟**還原資料庫** 對話方塊 (按一下**還原**上**工作**小工具)。

2. 選取 **備份檔案**中**從還原**欄位。 

3. 按一下省略符號 （...），在**備份檔案路徑**欄位，然後選取最新的備份檔案*TutorialDB*。

3. 型別**TutorialDB_Restored**中**目標資料庫**欄位中**目的地**一節，以將備份檔案還原至新的資料庫。

   ![還原](./media/tutorial-backup-restore-sql-server/restore.png)

4. 按一下 **還原**

5. 若要檢視還原作業的狀態，請按**CTRL + T**來開啟**工作歷程記錄**資訊看板。

   ![還原](./media/tutorial-backup-restore-sql-server/task-history-restore.png)


在本教學課程中，您已了解如何：
> [!div class="checklist"]
> * 備份資料庫 
> * 檢視備份狀態
> * 產生用來執行備份的指令碼
> * 還原資料庫
> * 檢視還原工作的狀態

