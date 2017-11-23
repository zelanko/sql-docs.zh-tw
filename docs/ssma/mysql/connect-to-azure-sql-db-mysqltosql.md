---
title: "連接到 Azure SQL DB (MySQLToSQL) |Microsoft 文件"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 81623d27-25af-444f-9779-1edb8c6fb470
caps.latest.revision: "8"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 743b17ae379d4b4b4f0a040f8035d80ced230cf0
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="connect-to-azure-sql-db-mysqltosql"></a>連接到 Azure SQL DB (MySQLToSQL)
使用 [連線到 SQL Azure] 對話方塊中，連接到您想要移轉 SQL Azure 資料庫。  
  
若要存取此對話方塊，請在**檔案**功能表上，選取**連接到 SQL Azure**。 如果您之前已連線，則命令是**重新連接到 SQL Azure。**  
  
## <a name="options"></a>選項。  
**伺服器名稱**  
  
選取或輸入伺服器名稱來連接到 SQL Azure。  
  
**資料庫**  
  
選取、 輸入或**瀏覽**資料庫名稱。  
  
> [!IMPORTANT]  
> SSMA for MySQL 不支援 SQL Azure 中的 master 資料庫的連接。  
  
**使用者名稱**  
  
輸入 SSMA 將用來連接到 SQL Azure 資料庫的使用者名稱  
  
**密碼**  
  
請輸入使用者名稱的密碼。  
  
**加密**  
  
SSMA 會建議加密的連接到 SQL Azure。  
  
## <a name="create-azure-database"></a>建立 Azure 的資料庫  
如果沒有 SQL Azure 帳戶中的資料庫，您可以建立第一個資料庫。  
  
若要建立新的資料庫非常第一次，請遵循下列步驟  
  
1.  按一下 [瀏覽] 按鈕會出現在 [連接到 SQL Azure] 對話方塊  
  
2.  如果沒有資料庫，則會出現下列兩個功能表項目。  
  
    1.  **（找不到資料庫）**是停用，隨時都呈現灰色  
  
    2.  **建立新的資料庫**這在只有當 SQL Azure 帳戶上沒有資料庫時，才會啟用。 按一下這個功能表項目，建立 Azure 資料庫 對話方塊才會出現在資料庫的名稱和大小。  
  
3.  在建立資料庫時，下列兩個參數提供做為輸入：  
  
    1.  **資料庫名稱：**輸入資料庫名稱。  
  
    2.  **資料庫大小：**選取您要在 SQL Azure 帳戶中建立的資料庫大小。  
  
