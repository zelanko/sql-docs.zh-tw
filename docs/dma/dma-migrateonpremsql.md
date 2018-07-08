---
title: 移轉內部部署 SQL Server 使用資料移轉小幫手 |Microsoft Docs
description: 了解如何使用 Data Migration Assistant 移轉內部部署 SQL Server，另一個 SQL Server 或 Azure SQL Database
ms.custom: ''
ms.date: 09/01/2017
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.suite: sql
ms.technology: dma
ms.tgt_pltfrm: ''
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, on-premises SQL Server
ms.assetid: ''
caps.latest.revision: ''
author: HJToland3
ms.author: jtoland
manager: craigg
ms.openlocfilehash: 8133b4176fc8f8197cab646d51f4ece68b6250bc
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/04/2018
ms.locfileid: "37784809"
---
# <a name="migrate-an-on-premises-sql-server-with-data-migration-assistant"></a>將資料移轉小幫手使用內部部署 SQL Server 移轉

本文提供將 SQL Server 移轉的逐步指示，使用 Data Migration Assistant。 Data Migration Assistant 可提供無縫式的評估和現代化內部部署 SQL Server 和 SQL Azure VM 的資料平台，以及 Azure SQL Database 的移轉作業。  

若要執行移轉時，完成下列工作。

- [建立新的移轉專案](#create-a-new-migration-project)
- [指定的來源和目標](#specify-source-and-target)
- [新增資料庫](#add-databases)
- [選取 登入](#select-logins)

## <a name="create-a-new-migration-project"></a>建立新的移轉專案

1. 按一下 **的新**（+） 的左的窗格，然後選取**移轉**專案類型。

1. 若要設定來源和目標伺服器類型**SQL Server**如果您要升級到的內部部署 SQL Server 執行現代化內部部署 SQL Server。

1. 按一下 **[建立]**。

   ![建立移轉專案](../dma/media/NewCreate.png)

## <a name="specify-the-source-and-target"></a>指定的來源和目標

1. 做為來源，請輸入中的 SQL Server 執行個體名稱**伺服器名稱**欄位中**來源伺服器詳細資料**一節。 

1. 選取 **驗證類型**來源 SQL Server 執行個體所支援。

1. 針對目標中，輸入 SQL Server 執行個體名稱**伺服器名稱**欄位中**目標伺服器詳細資料**一節。 

1. 選取 **驗證類型**目標 SQL Server 執行個體所支援。

1. 建議您選取加密的連接**加密連接**中**連接屬性**一節。

1. 按 [下一步] 。

   ![指定來源和目標頁面](../dma/media/SourceTarget.png)

## <a name="add-databases"></a>新增資料庫

1. 選擇您想要只在左窗格中選取這些資料庫，移轉的特定資料庫**將資料庫新增**頁面。

   依預設，來源 SQL Server 執行個體上的所有使用者資料庫會都選取進行移轉

1. 使用頁面右邊的移轉設定，來設定會套用到資料庫，執行下列移轉選項。

   > [!NOTE]
   > 您可以套用移轉設定至您要移轉，在左窗格中選取伺服器的所有資料庫。 您也可以在左窗格中選取資料庫，來設定具有特定設定的個別資料庫。

 1. 指定**共用的備份作業的來源和目標 SQL server 可存取位置**。 請確定執行來源的服務帳戶 SQL Server 執行個體具有寫入權限的共用位置，而且目標服務帳戶有讀取共用位置上的權限。

 1. 指定要還原的資料和目標伺服器上的交易記錄檔的位置。

    ![新增資料庫 頁面](../dma/media/AddDatabases.png)

1. 輸入來源和目標 SQL Server 執行個體，具有存取權，在共用的位置**共用位置選項** 方塊中。

1. 如果您無法提供的共用的位置的來源和目標 SQL Server 存取，請選取**將資料庫備份複製到目標伺服器可以讀取及從中還原的不同位置**。 然後，輸入的值**還原選項的備份位置** 方塊中。 

   請確定執行 Data Migration Assistant 的使用者帳戶具有讀取權限，才能備份的位置，並從中還原目標伺服器位置的寫入權限。

   ![若要將資料庫備份複製到不同位置的選項](../dma/media/CopyDatabaseDifferentLocation.png)

1. 按 [下一步] 。

資料移轉小幫手會執行驗證之備份的資料夾中，資料和記錄檔位置。 如果任何驗證失敗，請修正選項並按一下**下一步**。

## <a name="select-logins"></a>選取 登入

1. 選取特定的登入進行移轉。

   > [!IMPORTANT]
   > 請務必選取對應至在選取要移轉的資料庫中的一或多個使用者的登入。   

   根據預設，會選取要移轉的符合移轉資格的所有 SQL Server 和 Windows 登入。

1. 按一下 **開始移轉**。

   ![選取 登入，並開始移轉](../dma/media/SelectLogins.png)

## <a name="view-results"></a>檢視結果

您可以在監視移轉進度**檢視結果**頁面。

![檢視結果 頁面](../dma/media/ViewResults.png)

## <a name="export-migration-results"></a>匯出移轉結果

1. 按一下 **將報表匯出**底部**檢視結果**頁面，即可將移轉的結果儲存至 CSV 檔案。

1. 檢閱儲存的檔案，如需登入移轉時，詳細資訊，並確認所做的變更。

## <a name="see-also"></a>另請參閱

[Data Migration Assistant (DMA)](../dma/dma-overview.md)

[資料移轉小幫手： 組態設定](../dma/dma-configurationsettings.md)

[資料移轉小幫手： 最佳做法](../dma/dma-bestpractices.md)
