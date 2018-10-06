---
title: 移轉內部部署 SQL Server 或 Azure Vm 上的 SQL Server 到 Azure SQL Database 使用 Data Migration Assistant |Microsoft Docs
description: 了解如何使用 Data Migration Assistant 將內部部署 SQL Server 移轉至 Azure SQL Database
ms.custom: ''
ms.date: 10/05/2018
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
ms.author: rajpo
manager: craigg
ms.openlocfilehash: cd2fbf4340978424816ba3b4577e7559d80ea68c
ms.sourcegitcommit: 2da0c34f981c83d7f1d37435c80aea9d489724d1
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/04/2018
ms.locfileid: "48782387"
---
# <a name="migrate-on-premises-sql-server-or-sql-server-on-azure-vms-to-azure-sql-database-using-the-data-migration-assistant"></a>將內部部署 SQL Server 或 Azure Vm 上的 SQL Server 移轉至 Azure SQL Database 使用 Data Migration Assistant

Data Migration Assistant 中提供無縫式的評估，SQL Server 內部部署和更新版本的 SQL Server 的升級或移轉至 SQL Server 的 Azure Vm 或 Azure SQL Database。

這篇文章會提供至 Azure SQL Database 移轉 SQL Server 內部部署的逐步指示，使用 Data Migration Assistant。   

## <a name="create-a-new-migration-project"></a>建立新的移轉專案

1. 在左窗格中，選取**的新**（+），然後選取**移轉**專案類型。

2. 將來源類型設定為**SQL Server**和目標伺服器類型**Azure SQL Database**。

3. 選取 [建立]。

   ![建立移轉專案](../dma/media/NewCreate1.png)

## <a name="specify-the-source-server-and-database"></a>指定來源伺服器和資料庫

1. 做為來源，底下**連接到來源伺服器**，請在**伺服器名稱**文字中，輸入來源 SQL Server 執行個體的名稱。

2. 選取 **驗證類型**來源 SQL Server 執行個體所支援。

   > [!NOTE]
   > 它是您選取加密的連接 recommedned**加密連接**下方的核取方塊**連線 poperties**。

    ![選取來源伺服器](../dma/media/select-source-server.png)

3. 選取 [連接]。

4. 選取要移轉至 Azure SQL Database 的單一來源資料庫。

   > [!NOTE]
   > 如果您想要評估的資料庫和檢視，並套用建議的移轉，選取之前，先修復**移轉之前，先評估資料庫？** 核取方塊。

    ![選取來源資料庫](../dma/media/select-source-database.png)

5. 選取 **[下一步]**。

## <a name="specify-the-target-server-and-database"></a>指定目標伺服器和資料庫

1. 目標，如底下**連接到目標伺服器**，請在**伺服器名稱**文字方塊中，輸入 Azure SQL Database 執行個體的名稱。 

2. 選取 **驗證類型**目標 Azure SQL Database 執行個體所支援。

   > [!NOTE]
   > 它是您選取加密的連接 recommedned**加密連接**下方的核取方塊**連線 poperties**。

     ![選取目標伺服器](../dma/media/select-target-server.png)

3. 選取 [連接]。

4. 選取要移轉至單一目標資料庫。

   > [!NOTE]
   > 如果您想要將移轉中的 Windows 使用者**目標外部使用者網域名稱**文字，請確定已正確指定目標外部使用者網域名稱。

    ![選取目標資料庫](../dma/media/select-target-database.png)

5. 選取 **[下一步]**。

## <a name="select-schema-objects"></a>選取結構描述物件

1.  選取的結構描述物件從來源資料庫中，您想要移轉到 Azure SQL Database。

    ![選取結構描述物件](../dma/media/select-schema-objects.png)

       > [!NOTE]
       > 某些物件無法轉換為-是會自動修正的機會。 在右窗格中，按一下左窗格上的這些物件顯示建議的修正。 檢閱修正程式，並選擇要套用或忽略所有的變更，物件的物件。 請注意，套用或忽略所有變更的物件不會影響其他資料庫物件的變更。 無法轉換或自動修正的陳述式會重製到目標資料庫，並加上註解。

    ![建議的修正程式](../dma/media/suggested-fix.png)

2. 選取 **一般 SQL 指令碼**。
 
3. 檢閱產生的指令碼。

    ![產生的指令碼](../dma/media/generated-script.png)

## <a name="deploy-schema"></a>部署結構描述

1. 選取 **部署結構描述**。

2. 檢閱結構描述部署的結果。
 
    ![結構描述部署結果](../dma/media/schema-deployment-results.png)

3. 選取 **將資料移轉**啟動資料移轉程序。
 
4. 選取您想要移轉的資料的資料表。

    ![選取要移轉的資料表](../dma/media/select-tables-to-migrate.png) 

5. 選取 **啟動資料移轉**。
 
最後一個畫面會顯示整體狀態。

   ![移轉狀態](../dma/media/migration-status.png) 

## <a name="see-also"></a>另請參閱

- [Data Migration Assistant (DMA)](../dma/dma-overview.md)
- [資料移轉小幫手： 組態設定](../dma/dma-configurationsettings.md)
- [資料移轉小幫手： 最佳做法](../dma/dma-bestpractices.md)
