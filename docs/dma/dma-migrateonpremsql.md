---
title: 升級內部部署 SQL Server 到 SQL Server 或 SQL Server Azure Vm 上使用資料移轉小幫手 |Microsoft Docs
description: 了解如何使用 Data Migration Assistant 將升級至較新版的 SQL Server 或 Azure Vm 上的 SQL Server 的內部部署 SQL Server
ms.custom: ''
ms.date: 10/20/2018
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, on-premises SQL Server
ms.assetid: ''
author: pochiraju
ms.author: rajpo
manager: craigg
ms.openlocfilehash: e0d3ee1784653205feb4aa95a80a82d5ac27ec46
ms.sourcegitcommit: 38f35b2f7a226ded447edc6a36665eaa0376e06e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/23/2018
ms.locfileid: "49643836"
---
# <a name="upgrade-on-premises-sql-server-to-sql-server-or-sql-server-on-azure-vms-using-the-data-migration-assistant"></a>在內部部署 SQL Server 升級至 SQL Server 或 SQL Server Azure Vm 上使用 Data Migration Assistant

Data Migration Assistant 中提供無縫式的評估，SQL Server 內部部署和更新版本的 SQL Server 的升級或移轉至 SQL Server 的 Azure Vm 或 Azure SQL Database。

本文提供使用 Data Migration Assistant 較新版本的 SQL Server 或 Azure Vm 上的 SQL Server 升級 SQL Server 內部部署的逐步指示。   

## <a name="create-a-new-migration-project"></a>建立新的移轉專案

1. 在左窗格中，選取**的新**（+），然後**移轉**專案類型。

2. 若要設定來源和目標伺服器類型**SQL Server**如果您要升級內部部署 SQL Server 的內部部署 SQL Server 更新版本。

3. 選取 [建立]。

   ![建立移轉專案](../dma/media/NewCreate.png)

## <a name="specify-the-source-and-target"></a>指定的來源和目標

1. 做為來源，請輸入中的 SQL Server 執行個體名稱**伺服器名稱**欄位中**來源伺服器詳細資料**一節。 

2. 選取 **驗證類型**來源 SQL Server 執行個體所支援。

3. 針對目標中，輸入 SQL Server 執行個體名稱**伺服器名稱**欄位中**目標伺服器詳細資料**一節。 

4. 選取 **驗證類型**目標 SQL Server 執行個體所支援。

5. 建議您選取加密的連接**加密連接**中**連接屬性**一節。

6. 按 [下一步] 。

   ![指定來源和目標頁面](../dma/media/SourceTarget.png)

## <a name="add-databases"></a>新增資料庫

1. 選擇您想要只在左窗格中選取這些資料庫，移轉的特定資料庫**將資料庫新增**頁面。

   依預設，來源 SQL Server 執行個體上的所有使用者資料庫會都選取進行移轉

2. 使用頁面右邊的移轉設定，來設定會套用到資料庫，執行下列移轉選項。

   > [!NOTE]
   > 您可以套用移轉設定至您要移轉，在左窗格中選取伺服器的所有資料庫。 您也可以在左窗格中選取資料庫，來設定具有特定設定的個別資料庫。

    A. 指定**共用的備份作業的來源和目標 SQL server 可存取位置**。 請確定執行來源的服務帳戶 SQL Server 執行個體具有寫入權限的共用位置，而且目標服務帳戶有讀取共用位置上的權限。

    B. 指定要還原的資料和目標伺服器上的交易記錄檔的位置。

    ![新增資料庫 頁面](../dma/media/AddDatabases.png)

3. 輸入來源和目標 SQL Server 執行個體，具有存取權，在共用的位置**共用位置選項** 方塊中。

4. 如果您無法提供的共用的位置的來源和目標 SQL Server 存取，請選取**將資料庫備份複製到目標伺服器可以讀取及從中還原的不同位置**。 然後，輸入的值**還原選項的備份位置** 方塊中。 

   請確定執行 Data Migration Assistant 的使用者帳戶具有讀取權限，才能備份的位置，並從中還原目標伺服器位置的寫入權限。

   ![若要將資料庫備份複製到不同位置的選項](../dma/media/CopyDatabaseDifferentLocation.png)

5. 選取 **[下一步]**。

Data Migration Assistant 上備份的資料夾、 資料和記錄檔位置執行驗證。 如果任何驗證失敗，修正選項，然後按**下一步**。

## <a name="select-logins"></a>選取 登入

1. 選取特定的登入進行移轉。

   > [!IMPORTANT]
   > 請務必選取對應至在選取要移轉的資料庫中的一或多個使用者的登入。   

   根據預設，會選取要移轉的符合移轉資格的所有 SQL Server 和 Windows 登入。

2. 選取 **開始移轉**。

   ![選取 登入，並開始移轉](../dma/media/SelectLogins.png)

## <a name="view-results"></a>檢視結果

您可以在監視移轉進度**檢視結果**頁面。

![檢視結果 頁面](../dma/media/ViewResults.png)

## <a name="export-migration-results"></a>匯出移轉結果

1. 按一下 **將報表匯出**底部**檢視結果**頁面，即可將移轉的結果儲存至 CSV 檔案。

2. 檢閱儲存的檔案，如需登入移轉時，詳細資訊，並確認所做的變更。

## <a name="see-also"></a>另請參閱

- [Data Migration Assistant (DMA)](../dma/dma-overview.md)
- [資料移轉小幫手： 組態設定](../dma/dma-configurationsettings.md)
- [資料移轉小幫手： 最佳做法](../dma/dma-bestpractices.md)
