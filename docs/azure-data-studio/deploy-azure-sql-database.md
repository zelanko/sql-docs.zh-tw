---
title: 透過筆記本部署 Azure SQL Database
description: 本教學課程示範如何建立 Azure SQL Database。
author: ninarn
ms.author: ninarn
ms.reviewer: alayu, markingmyname
ms.topic: tutorial
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.custom: ''
ms.date: 10/16/2020
ms.openlocfilehash: 5b68bda566bdd28c8dd2e70f036dd8e17643f776
ms.sourcegitcommit: 43b92518c5848489d03c68505bd9905f8686cbc0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/17/2020
ms.locfileid: "92155026"
---
# <a name="create-an-azure-sql-database-using-azure-data-studio"></a>使用 Azure Data Studio 建立 Azure SQL Database

您可透過部署精靈和筆記本，使用 Azure Data Studio 建立 Azure SQL Database。

## <a name="pre-requisites"></a>必要條件

 - 已安裝 [Azure Data Studio](download-azure-data-studio.md)
 - 作用中的 Azure 帳戶和訂閱。 如果您沒有帳戶，請[建立免費帳戶](https://azure.microsoft.com/free/)。

## <a name="use-the-deployment-wizard"></a>使用部署精靈

請遵循下列步驟使用部署精靈，這會引導您完成簡單 UI 體驗的必要設定。

首先，在部署精靈中尋找並選取 Azure SQL 資料庫。

 1. 在 Azure Data Studio 中，選取左側導覽中的 [連線] viewlet。
 2. 選取 [連線] 面板頂端的 [...] 按鈕，然後選擇 [新增部署]。
 3. 在部署精靈中，選取 [Azure SQL Database] 磚，然後勾選 [接受條款] 核取方塊
 4. 在 [資源類型] 下拉式清單中，選取您想要建立的項目 - 資料庫、資料庫伺服器或彈性集區。 如果您在 Azure 中沒有任何 SQL 資料庫，則建議先從建立資料庫開始。
 5. 如果要建立伺服器或集區，請選取 [在 Azure 入口網站中建立]；如果要建立資料庫，請選取 [選取]。

如果要建立資料庫，請遵循下列步驟。

 1. 如果尚未登入 Azure 帳戶，請登入。 如果在此精靈頁面上遇到問題，您可重新整理連線。
 2. 選取想要的訂用帳戶和伺服器。 然後選取 [下一步]  。
 3. 輸入資料庫名稱。
 4. 輸入執行 Azure Data Studio 本機用戶端電腦的防火牆規則名稱與 IP 範圍。 在其建立後，即可立即從 ADS 連線到伺服器和資料庫。
 5. 選取 [下一步] 。
 6. 檢閱所輸入的參數，然後選取 [將指令碼編寫至筆記本]。

筆記本開啟之後，您就可以檢閱內容和程式碼，並隨意變更。 您在效能或費用上如有特定的喜好設定，可變更預設的計算與儲存設定。 但請注意，您對筆記本進行的任何變更都可能會導致驗證錯誤。

最後一個步驟是選取 [全部執行]，以執行筆記本中的所有資料格。 完成後，您應該會有一個完整建立且正在執行的 SQL 資料庫，您可從 ADS 與其連線並進行查詢。

## <a name="next-steps"></a>後續步驟

建立資料庫、伺服器或集區之後，您可在 Azure Data Studio 中[連線及查詢](quickstart-sql-database.md)資料庫。
