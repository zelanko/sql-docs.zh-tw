---
title: 執行 SQL Server 整合服務遷移評估（Data Migration Assistant） |Microsoft Docs
description: 瞭解如何在遷移至 Azure SQL Database 或 Azure SQL Database 受控實例之前，使用 Data Migration Assistant 來評估內部部署 SQL Server 整合服務
ms.custom: ''
ms.date: 08/23/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Assess
ms.assetid: ''
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 84b498cbaf7a2f3d1118894157c17b8270259afa
ms.sourcegitcommit: 66dbc3b740f4174f3364ba6b68bc8df1e941050f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/05/2019
ms.locfileid: "73632873"
---
# <a name="perform-a-sql-server-integration-service-migration-assessment-with-data-migration-assistant"></a>使用 Data Migration Assistant 執行 SQL Server 整合服務遷移評估

下列逐步指示可協助您執行第一次評估，使用 Data Migration Assistant 將 SQL Server 整合服務（SSIS）封裝遷移至 Azure SQL Database 或 Azure SQL Database 受控實例。

## <a name="create-an-assessment"></a>建立評量

1. 選取 [**新增**] （+）圖示，然後選取 [**評估**] 專案類型作為 [**整合服務**]。

1. 設定來源和目標伺服器類型。

    選取 來源 做為  **SQL Server**，並將 目標伺服器類型 設定為  **Azure SQL Database**  或**Azure SQL Database 受控實例**。

1. 按一下 **[建立]** 。

    ![建立評量](media/dma-assess-ssis/dma-assess-ssis-create.png)

## <a name="connect-to-a-server"></a>連接到伺服器

1. 遵循預設選項，然後按 **[下一步] [** **選取來源**]。
1. 輸入 SQL server 實例名稱，選擇 [驗證類型]，並設定正確的連接屬性。
1. 選擇性輸入包含 SSIS 封裝的資料夾路徑。
1. 選擇性輸入套件加密密碼（如果適用的話）。
1. 按一下 [連接到來源 SQL server **]** 。
  ![新增來源](media/dma-assess-ssis/dma-assess-ssis-addsource.png)

## <a name="add-sources-to-assess"></a>新增要評估的來源

1. 選取要評估的 SSIS 套件儲存類型，然後選取 [**新增**]。
![新增來源](media/dma-assess-ssis/dma-assess-ssis-addsource-type.png)
1. 如果需要評估多個資料夾，請選取 [**新增來源**] 以開啟 [連線] 飛出視窗功能表。
1. 按一下 [**開始評估**]。
  ![開始評估](media/dma-assess-ssis/dma-assess-ssis-assess.png)

## <a name="view-results"></a>檢視結果

相容性問題類別提供部分支援或不支援的功能，會封鎖將內部部署 SSIS 套件遷移至 Azure SSIS Integration Runtime。 接著，它會提供可協助您解決這些問題的建議。

![檢視結果](media/dma-assess-ssis/dma-assess-ssis-result.png)

## <a name="next-steps"></a>後續的步驟

- [將內部部署 SSIS 工作負載遷移至 ADF 中的 SSIS 總覽](https://docs.microsoft.com/azure/data-factory/scenario-ssis-migration-overview)
- [將 SQL Server Integration Services 封裝遷移至 Azure SQL Database 受控實例](https://docs.microsoft.com/azure/dms/how-to-migrate-ssis-packages-managed-instance)
- [將 SQL Server Integration Services 封裝重新部署至 Azure SQL Database](https://docs.microsoft.com/azure/dms/how-to-migrate-ssis-packages)
