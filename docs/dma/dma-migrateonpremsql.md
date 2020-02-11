---
title: 使用 Data Migration Assistant 升級 SQL Server
description: 瞭解如何使用 Data Migration Assistant 將內部部署 SQL Server 升級至較新版本的 SQL Server 或 Azure Vm 上的 SQL Server
ms.custom: seo-lt-2019
ms.date: 05/18/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, on-premises SQL Server
ms.assetid: ''
author: HJToland3
ms.author: jtoland
ms.openlocfilehash: fc78354e3b422342e376bd7ebe75233dcd3ffaee
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "74056528"
---
# <a name="upgrade-sql-server-using-the-data-migration-assistant"></a>使用 Data Migration Assistant 升級 SQL Server

Data Migration Assistant 提供 SQL Server 內部部署的順暢評量，並升級至較新版本的 SQL Server 或遷移至 Azure Vm 或 Azure SQL Database 上的 SQL Server。

本文提供逐步指示，說明如何將 SQL Server 內部部署升級至 SQL Server 的較新版本，或使用 Data Migration Assistant 在 Azure Vm 上 SQL Server。

## <a name="create-a-new-migration-project"></a>建立新的移轉專案

1. 在左窗格中，依序選取 [**新增**（+）] 和 [**遷移**] 專案類型。

2. 如果您要將內部部署 SQL Server 升級至較新版本的內部部署 SQL Server，請將來源和目標伺服器類型設定為**SQL Server** 。

3. 選取 [建立]  。

   ![建立遷移專案](../dma/media/NewCreate.png)

## <a name="specify-the-source-and-target"></a>指定來源和目標

1. 針對 [來源]，在 [**來源伺服器詳細資料**] 區段的 [**伺服器名稱**] 欄位中輸入 SQL Server 實例名稱。 

2. 選取來源 SQL Server 實例所支援的**驗證類型**。

3. 針對 [目標]，在 [**目標伺服器詳細資料**] 區段的 [**伺服器名稱**] 欄位中輸入 SQL Server 實例名稱。 

4. 選取目標 SQL Server 實例所支援的**驗證類型**。

5. 建議您在 [連線**屬性**] 區段中選取 [**加密連接**]，以加密連接。

6. 按 [下一步]  。

   ![指定來源和目標頁面](../dma/media/SourceTarget.png)

## <a name="add-databases"></a>新增資料庫

1. 在 [**新增資料庫**] 頁面的左窗格中，選擇您想要遷移的特定資料庫，只選取這些資料庫。

   根據預設，會選取來源 SQL Server 實例上的所有使用者資料庫進行遷移

2. 使用頁面右側的 [遷移設定] 來設定要套用至資料庫的遷移選項，方法是執行下列動作。

   > [!NOTE]
   > 您可以在左窗格中選取伺服器，將遷移設定套用到您要遷移的所有資料庫。 您也可以在左窗格中選取資料庫，以設定具有特定設定的個別資料庫。

    a. 指定**用於備份作業的來源和目標 SQL server 可存取的共用位置**。 請確定執行來源 SQL Server 實例的服務帳戶具有共用位置的寫入權限，而目標服務帳戶對共用位置具有讀取權限。

    b. 指定要在目標伺服器上還原資料和交易式記錄檔的位置。

    ![[新增資料庫] 頁面](../dma/media/AddDatabases.png)

3. 在 [**共用位置選項**] 方塊中，輸入來源和目標 SQL Server 實例可存取的共用位置。

4. 如果您無法提供來源和目標 SQL Server 都能存取的共用位置，請選取 [**將資料庫備份複製到目標伺服器可以讀取和還原的不同位置**]。 然後，針對 [**還原的備份位置] 選項**方塊輸入值。 

   請確定執行 Data Migration Assistant 的使用者帳戶具有備份位置的讀取權限，以及目標伺服器還原之位置的寫入權限。

   ![將資料庫備份複製到不同位置的選項](../dma/media/CopyDatabaseDifferentLocation.png)

5. 選取 [下一步]  。

Data Migration Assistant 會在備份檔案夾、資料和記錄檔位置上執行驗證。 如果驗證失敗，請修正選項，然後選取 **[下一步]**。

## <a name="select-logins"></a>選取登入

1. 選取要進行遷移的特定登入。

   > [!IMPORTANT]
   > 請務必選取對應到所選資料庫中一或多個使用者的登入，以進行遷移。   

   根據預設，會選取所有符合遷移資格的 SQL Server 和 Windows 登入來進行遷移。

2. 選取 [**開始遷移**]。

   ![選取登入並開始遷移](../dma/media/SelectLogins.png)

## <a name="view-results"></a>檢視結果

您可以在 [**查看結果**] 頁面上監視遷移進度。

![[查看結果] 頁面](../dma/media/ViewResults.png)

## <a name="export-migration-results"></a>匯出遷移結果

1. 按一下 [**視圖結果**] 頁面底部的 [**匯出報表**]，將遷移結果儲存到 CSV 檔案。

2. 檢查已儲存的檔案，以取得有關登入遷移的詳細資料，然後驗證變更。

## <a name="see-also"></a>另請參閱

- [Data Migration Assistant (DMA)](../dma/dma-overview.md)
- [Data Migration Assistant：設定](../dma/dma-configurationsettings.md)
- [Data Migration Assistant：最佳做法](../dma/dma-bestpractices.md)
