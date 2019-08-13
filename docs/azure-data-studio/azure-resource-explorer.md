---
title: 使用 Azure 資源總管探索 Azure SQL 資源
titleSuffix: Azure Data Studio
description: 了解如何透過 Azure 資源總管，探索和管理 Azure SQL Server、Azure SQL Database 和 Azure SQL 受控執行個體。
ms.custom: seodec18
author: yanancai
ms.author: yanacai
ms.date: 09/24/2018
ms.topic: quickstart
ms.prod: sql
ms.technology: azure-data-studio
ms.openlocfilehash: 87a0364555b9da22c89470965c281b3d939b6f4f
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/25/2019
ms.locfileid: "67959710"
---
# <a name="explore-and-manage-azure-sql-resources-with-azure-resource-explorer"></a>使用 Azure 資源總管探索和管理 Azure SQL 資源

在本文件中，您將了解如何透過 [!INCLUDE [Azure Data Studio](../includes/name-sos-short.md)] 中的 Azure 資源總管，探索和管理 Azure SQL Server、Azure SQL Database 和 Azure SQL 受控執行個體資源。

>[!NOTE]
>從 10 月開始，SQL Server 2019 Preview 將支援 Azure 資源總管。 之後，您可以透過[延伸模組管理員](extensions.md)，或透過 [檔案]   > [Install Package from VSIX Package] \(從 VSIX 套件安裝套件\)  ，安裝預覽版的延伸模組。


## <a name="connect-to-azure"></a>連線到 Azure

安裝 SQL 預覽版的外掛程式之後，Azure 圖示會出現在左側功能表列中。 按一下圖示即可開啟 Azure 資源總管。 如果您看不到 Azure 圖示，請以滑鼠右鍵按一下左側功能表列，然後選取 [Azure 資源總管]  。

### <a name="add-an-azure-account"></a>新增 Azure 帳戶

若要檢視與 Azure 帳戶相關聯的 SQL 資源，您必須先將帳戶新增至 [!INCLUDE [Azure Data Studio](../includes/name-sos-short.md)]。

1. 透過左下方的帳戶管理圖示，或透過 Azure 資源總管中的 [登入 Azure...]  連結，開啟 [連結的帳戶]  對話方塊。

    ![登入 Azure](media/azure-resource-explorer/sign-in-to-azure.png)

2. 在 [連結的帳戶]  對話方塊中，按一下 [新增帳戶]  。

    ![新增 Azure 帳戶](media/azure-resource-explorer/add-an-azure-account.png)

3. 按一下 [Copy and Open] \(複製與開啟\)  ，開啟瀏覽器進行驗證。

    ![在瀏覽器中開啟驗證頁面](media/azure-resource-explorer/open-authentication-in-browser.png)

4. 將**使用者程式碼**貼到網頁，然後按一下 [繼續]  進行驗證。

    ![在瀏覽器中驗證](media/azure-resource-explorer/authenticate-in-browser.png)

5. 在 [!INCLUDE [Azure Data Studio](../includes/name-sos-short.md)] 中，您現在應該會在 [連結的帳戶]  對話方塊中找到已登入的 Azure 帳戶。

    ![已登入的 Azure 帳戶](media/azure-resource-explorer/signed-in-azure-account.png)

### <a name="add-more-azure-accounts"></a>新增更多 Azure 帳戶

[!INCLUDE [Azure Data Studio](../includes/name-sos-short.md)] 支援多個 Azure 帳戶。 若要新增更多 Azure 帳戶，請按一下 [連結的帳戶]  對話方塊右上方的按鈕，並遵循與＜新增 Azure 帳戶＞一節同樣的步驟來新增更多 Azure 帳戶。

![新增更多 Azure 帳戶](media/azure-resource-explorer/add-more-azure-account.png)

### <a name="remove-an-azure-account"></a>移除 Azure 帳戶

若要移除現有的已登入 Azure 帳戶：

1. 透過左下方的帳戶管理圖示，開啟 [連結的帳戶]  對話方塊。
2. 按一下 Azure 帳戶右側的 [X]  按鈕，予以移除。

    ![移除 Azure 帳戶](media/azure-resource-explorer/remove-azure-account.png)

## <a name="filter-subscription"></a>篩選訂閱

登入 Azure 帳戶之後，所有與該 Azure 帳戶相關聯的訂閱都會顯示在 Azure 資源總管中。 您可以篩選每個 Azure 帳戶的訂閱。

1. 按一下 Azure 帳戶右側的 [選取訂閱]  按鈕。

   ![篩選訂閱](media/azure-resource-explorer/filter-subscription.png)

2. 選取您要瀏覽之帳戶訂閱的核取方塊，然後按一下 [確定]  。

   ![選取訂閱](media/azure-resource-explorer/select-subscription.png)

## <a name="explore-azure-sql-resources"></a>探索 Azure SQL 資源

若要巡覽 Azure 資源總管中的 Azure SQL 資源，請展開 Azure 帳戶和資源類型群組。

Azure 資源總管目前支援 Azure SQL Server、Azure SQL Database 和 Azure SQL 受控執行個體。

## <a name="connect-to-azure-sql-resources"></a>連線到 Azure SQL 資源

Azure 資源總管提供快速存取，協助您連線到 SQL Server 和資料庫，進行查詢和管理。 

1. 從樹狀檢視探索您想要連線的 SQL 資源。
2. 以滑鼠右鍵按一下資源並選取 [連線]  ，您也可以在資源右側找到 [連線] 按鈕。

   ![連線到 Azure SQL 資源](media/azure-resource-explorer/connect-to-azure-sql-resource.png)

3. 在開啟的 [連線]  對話方塊中，輸入您的密碼，然後按一下 [連線]  。

   ![SQL 連線對話方塊](media/azure-resource-explorer/sql-connection-dialog.png)
4. 連線成功之後，[伺服器]  視窗會自動開啟新連線的 SQL 伺服器/資料庫。

## <a name="next-steps"></a>後續步驟

- [使用 [!INCLUDE[Azure Data Studio](../includes/name-sos-short.md)] 連線及查詢 Azure SQL Database](quickstart-sql-database.md)
- [使用 [!INCLUDE[Azure Data Studio](../includes/name-sos-short.md)] 連線及查詢 Azure SQL 資料倉儲中的資料](quickstart-sql-dw.md)