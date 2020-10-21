---
title: 透過筆記本部署 Azure SQL Database
description: 本教學課程示範如何建立 Azure SQL Database。
author: ninarn
ms.author: ninarn
ms.reviewer: alayu, maghan
ms.topic: tutorial
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.custom: ''
ms.date: 10/14/2020
ms.openlocfilehash: 88bb9fd980da21b20f0faf6f699147d26abe65b9
ms.sourcegitcommit: 76ab3b57718341c6057613c9bd38cf82fb17786e
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/14/2020
ms.locfileid: "92060865"
---
# <a name="create-an-azure-sql-database-using-azure-data-studio"></a>使用 Azure Data Studio 建立 Azure SQL Database

您可透過部署精靈和筆記本，使用 Azure Data Studio 建立 Azure SQL Database。

## <a name="pre-requisites"></a>必要條件

 - 已安裝 [Azure Data Studio](download-azure-data-studio.md)
 - 作用中的 Azure 帳戶和訂閱。 如果您沒有訂用帳戶，請[建立免費帳戶](https://azure.microsoft.com/free/)。

## <a name="use-the-deployment-wizard"></a>使用部署精靈

請遵循下列步驟使用部署精靈，這會引導您完成簡單 UI 體驗的必要設定。

首先，在部署精靈中尋找並選取 Azure SQL Database。

 1. 在 Azure Data Studio 中，選取左側導覽中的 [連線] viewlet。
 2. 選取 [連線] 面板頂端的 [...] 按鈕，然後選擇 [新增部署]。
 3. 在部署精靈中，選取 [Azure SQL Database] 磚，然後勾選 [接受條款] 核取方塊
 4. 在 [資源類型] 下拉式清單中，選取您想要建立的項目 - 資料庫、資料庫伺服器或彈性集區。 如果您在 Azure 中沒有任何 SQL 資料庫，建議您先從建立資料庫開始。
 5. 在 Azure 入口網站中選取 [建立]

接下來，輸入所有慣用設定以建立您的資料庫、伺服器或集區。 您可在 [Azure SQL 文件](https://docs.microsoft.com/azure/azure-sql/database/single-database-create-quickstart?tabs=azure-portal)中，找到一些如何設定這些設定的指引。

## <a name="next-steps"></a>後續步驟

建立資料庫、伺服器或集區之後，您可在 Azure Data Studio 中[連線及查詢](quickstart-sql-database.md)資料庫。
