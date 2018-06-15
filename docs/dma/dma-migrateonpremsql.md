---
title: 移轉內部部署 SQL Server （資料移轉小幫手） |Microsoft 文件
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
ms.openlocfilehash: b535e41b93d337fc2cc1ae3f12699dd841bf91b9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32868213"
---
# <a name="migrate-on-premises-sql-server-using-data-migration-assistant"></a>移轉內部部署 SQL Server 使用的資料移轉小幫手

本文將提供使用資料移轉小幫手移轉 SQL Server 的逐步指示。

資料移轉小幫手提供無縫式的評估和現代在內部部署 SQL Server 和 SQL Azure VM 的資料平台的移轉。  

完成下列工作來執行移轉。

- [建立新的移轉專案](#create-a-new-migration-project)
- [指定的來源和目標](#specify-source-and-target)
- [新增資料庫](#add-databases)
- [選取 登入](#select-logins)

## <a name="create-a-new-migration-project"></a>建立新的移轉專案

1. 按一下**新增**（+），然後選取左的窗格**移轉**專案類型。

1. 將來源和目標伺服器類型設為**SQL Server**如果您要升級至內部部署 SQL Server 現代化內部部署 SQL Server。

1. 按一下 **[建立]**。

   ![建立移轉專案](../dma/media/NewCreate.png)

## <a name="specify-the-source-and-target"></a>指定的來源和目標

1. 做為來源，請輸入中的 SQL Server 執行個體名稱**伺服器名稱**欄位**來源伺服器的詳細資料**> 一節。 

1. 選取**驗證類型**來源 SQL Server 執行個體所支援。

1. 目標中，輸入中的 SQL Server 執行個體名稱**伺服器名稱**欄位**目標伺服器詳細資料**> 一節。 

1. 選取**驗證類型**目標 SQL Server 執行個體所支援。

1. 建議您選取加密的連接**加密連接**中**連接屬性**> 一節。

1. 按一下 **[下一步]**。

   ![指定來源和目標 頁面](../dma/media/SourceTarget.png)

## <a name="add-databases"></a>新增資料庫

1. 選擇您想要移轉只選取這些資料庫，在左窗格中的特定資料庫**新增資料庫**頁面。

   依預設，來源 SQL Server 執行個體上的所有使用者資料庫會都選取進行移轉

1. 使用頁面右側的移轉設定，設定會套用到資料庫，藉由下列的移轉選項。

   > [!NOTE]
   > 您可以套用的移轉設定至您要移轉，在左窗格中選取伺服器的所有資料庫。 您也可以設定特殊設定個別資料庫，在左窗格中選取資料庫。


 1. 指定**由備份作業的來源和目標 SQL server 共用存取位置**。 請確定執行來源是服務帳戶 SQL Server 執行個體具有寫入權限的共用位置，而且目標服務帳戶有讀取共用位置上的權限。

 1. 指定要還原的資料和目標伺服器上的交易記錄檔的位置。

    ![新增資料庫 頁面](../dma/media/AddDatabases.png)

1. 輸入來源和目標 SQL Server 執行個體，具有存取權，在共用的位置**共用位置選項**方塊。

1. 如果您無法提供的共用的位置的來源和目標 SQL Server 存取，請選取**將資料庫備份複製到不同的位置，目標伺服器可以讀取，並從還原**。 然後，輸入一個值**還原選項的備份位置**方塊。 

   請確定執行資料移轉小幫手的使用者帳戶具有讀取權限的備份位置，並從中還原的目標伺服器位置的寫入權限。

   ![若要將資料庫備份複製到不同位置的選項](../dma/media/CopyDatabaseDifferentLocation.png)

1. 按一下 **[下一步]**。

資料移轉小幫手會執行驗證在備份的資料夾、 資料和記錄檔的位置。 如果任何驗證失敗，請修正選項並按一下**下一步**。

## <a name="select-logins"></a>選取 登入

1. 選取移轉的特定登入。

   > [!IMPORTANT]
   > 請務必選取對應至一或多個使用者在移轉所選的資料庫中的登入。   

   根據預設，移轉會選取符合移轉資格的所有 SQL Server 和 Windows 登入。

1. 按一下**開始移轉**。

   ![選取 登入和開始移轉](../dma/media/SelectLogins.png)

## <a name="view-results"></a>檢視結果

您可以監視移轉進度上**檢視結果**頁面。

![檢視結果 頁面](../dma/media/ViewResults.png)

## <a name="export-migration-results"></a>匯出移轉結果

1. 按一下**將報表匯出**底部**檢視結果**頁面，即可移轉將結果儲存到 CSV 檔案。

1. 檢閱儲存的檔案，如需詳細資訊和移轉相關的登入，並確認所做的變更。

## <a name="see-also"></a>另請參閱

[資料移轉小幫手 (DMA)](../dma/dma-overview.md)

[資料移轉小幫手： 組態設定](../dma/dma-configurationsettings.md)

[資料移轉小幫手： 最佳作法](../dma/dma-bestpractices.md)
