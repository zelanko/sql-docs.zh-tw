---
title: 探索使用 Azure 資源總管的 Azure SQL 資源
titleSuffix: Azure Data Studio
description: 了解如何瀏覽和管理 Azure SQL Server、 Azure SQL Database 和 Azure SQL 受控執行個體透過 Azure 資源總管。
ms.custom: seodec18
author: yanancai
ms.author: yanacai
ms.date: 09/24/2018
ms.topic: quickstart
ms.prod: sql
ms.technology: azure-data-studio
ms.openlocfilehash: 87a0364555b9da22c89470965c281b3d939b6f4f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67959710"
---
# <a name="explore-and-manage-azure-sql-resources-with-azure-resource-explorer"></a>瀏覽和管理 Azure SQL 資源使用 Azure 資源總管

本文件中，您將了解如何瀏覽和管理 Azure SQL Server、 Azure SQL database，以及透過 Azure 資源總管中的 Azure SQL 受控執行個體資源[!INCLUDE [Azure Data Studio](../includes/name-sos-short.md)]。

>[!NOTE]
>Azure 資源總管會在 SQL Server 於 2019 年 10 月預覽支援。 在那之後，您可以安裝預覽延伸模組，透過[延伸模組管理員](extensions.md)或透過**檔案** > **VSIX 封裝中的 安裝套件**。


## <a name="connect-to-azure"></a>連接到 Azure

安裝之後 SQL 預覽外掛程式，Azure 的圖示會出現在左側的功能表列。 按一下圖示以開啟 Azure 資源總管。 如果您沒有看到 [Azure] 圖示，以滑鼠右鍵按一下左側的功能表列，然後選取**Azure 資源總管**。

### <a name="add-an-azure-account"></a>新增 Azure 帳戶

若要檢視與 Azure 帳戶相關聯的 SQL 資源，您必須先將帳戶加入[!INCLUDE [Azure Data Studio](../includes/name-sos-short.md)]。

1. 開啟**連結的帳戶** 對話方塊，透過帳戶管理圖示在左下角，或透過**登入 Azure...** Azure 資源總管中的連結。

    ![登入 Azure](media/azure-resource-explorer/sign-in-to-azure.png)

2. 在 [**連結的帳戶**] 對話方塊中，按一下**新增帳戶**。

    ![新增 Azure 帳戶](media/azure-resource-explorer/add-an-azure-account.png)

3. 按一下 **複製並開啟**開啟瀏覽器進行驗證。

    ![在瀏覽器中開啟的驗證頁面](media/azure-resource-explorer/open-authentication-in-browser.png)

4. 貼上**使用者程式碼**在網頁上按一下**繼續**進行驗證。

    ![在瀏覽器中進行驗證](media/azure-resource-explorer/authenticate-in-browser.png)

5. 在 [!INCLUDE [Azure Data Studio](../includes/name-sos-short.md)]您現在應該會找到登入 Azure 帳戶中**連結帳戶**對話方塊。

    ![登入 Azure 帳戶](media/azure-resource-explorer/signed-in-azure-account.png)

### <a name="add-more-azure-accounts"></a>新增更多的 Azure 帳戶

中支援多個 Azure 帳戶[!INCLUDE [Azure Data Studio](../includes/name-sos-short.md)]。 若要新增更多的 Azure 帳戶，請按一下右上方按鈕**連結的帳戶**對話方塊，並遵循相同步驟以新增 Azure 帳戶 區段中新增更多的 Azure 帳戶。

![新增更多的 Azure 帳戶](media/azure-resource-explorer/add-more-azure-account.png)

### <a name="remove-an-azure-account"></a>移除 Azure 帳戶

若要移除現有的登入 Azure 帳戶：

1. 開啟**連結的帳戶**對話方塊透過左下角的帳戶管理圖示。
2. 按一下 [ **X** ] 按鈕，在 Azure 帳戶的權限，將它移除。

    ![移除 Azure 帳戶](media/azure-resource-explorer/remove-azure-account.png)

## <a name="filter-subscription"></a>篩選訂用帳戶

一旦登入 Azure 帳戶，所有訂用帳戶相關聯的 Azure 帳戶顯示在 Azure 資源總管中。 您可以篩選每個 Azure 帳戶的訂用帳戶。

1. 按一下 **選取的訂用帳戶**按鈕右邊的 Azure 帳戶。

   ![篩選訂用帳戶](media/azure-resource-explorer/filter-subscription.png)

2. 選取核取方塊，以瀏覽，然後按一下您想要的訂用帳戶**確定**。

   ![選取訂用帳戶](media/azure-resource-explorer/select-subscription.png)

## <a name="explore-azure-sql-resources"></a>探索 Azure SQL 資源

若要瀏覽 Azure SQL 資源在 Azure 資源總管中的，展開的 Azure 帳戶和資源類型的群組。

Azure 資源總管目前支援 Azure SQL Server、 Azure SQL Database 和 Azure SQL 受控執行個體。

## <a name="connect-to-azure-sql-resources"></a>連線到 Azure SQL 資源

Azure 資源總管會提供協助您連接到 SQL Server 和適用於查詢和管理資料庫的快速存取。 

1. 瀏覽您想要從樹狀檢視中使用連接的 SQL 資源。
2. 以滑鼠右鍵按一下資源，然後選取**Connect**，您也可以找到 [連接] 按鈕右邊的資源。

   ![連線到 Azure SQL 資源](media/azure-resource-explorer/connect-to-azure-sql-resource.png)

3. 在中開啟**連接** 對話方塊中，輸入您的密碼，然後按一下**Connect**。

   ![SQL 連線對話方塊](media/azure-resource-explorer/sql-connection-dialog.png)
4. **伺服器**視窗會自動使用新連接 SQL server/database 後開啟連線成功。

## <a name="next-steps"></a>後續步驟

- [使用[!INCLUDE[Azure Data Studio](../includes/name-sos-short.md)]連線及查詢 Azure SQL database](quickstart-sql-database.md)
- [使用[!INCLUDE[Azure Data Studio](../includes/name-sos-short.md)]連線及查詢 Azure SQL 資料倉儲中的資料](quickstart-sql-dw.md)