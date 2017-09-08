---
title: "連接到 Azure SQL DB (SybaseToSQL) |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 96538007-1099-40c8-9902-edd07c5620ee
caps.latest.revision: 5
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 76a29a448dfbbba4b8fc0771edf352545d361cf9
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="connect-to-azure-sql-db--sybasetosql"></a>連接到 Azure SQL DB (SybaseToSQL)
使用 [連線到 Azure SQL DB] 對話方塊中，連接到您想要移轉的 Azure SQL DB 資料庫。  
  
若要存取此對話方塊，請在**檔案**功能表上，選取**連接到 Azure SQL DB**。 如果您之前已連線，則命令是**重新連接到 Azure SQL DB。**  
  
## <a name="options"></a>選項  
**伺服器名稱**  
  
選取或輸入伺服器名稱連接到 Azure SQL DB。  
  
**資料庫**  
  
選取、 輸入或**瀏覽**資料庫名稱。  
  
> [!IMPORTANT]  
> SSMA for Sybase 不支援連接至 master 資料庫中 Azure SQL DB。  
  
**使用者名稱**  
  
輸入 SSMA 將用來連接到 Azure SQL DB 資料庫的使用者名稱  
  
**密碼**  
  
請輸入使用者名稱的密碼。  
  
**加密**  
  
SSMA 會建議加密的連接到 Azure SQL DB。  
  
## <a name="create-azure-database"></a>建立 Azure 的資料庫  
如果沒有在 Azure SQL DB 帳戶中的資料庫，您可以建立第一個資料庫。  
  
若要建立新的資料庫非常第一次，請遵循下列步驟  
  
1.  按一下 瀏覽 按鈕會出現在 連接到 Azure SQL DB 對話方塊  
  
2.  如果沒有資料庫，則會出現下列兩個功能表項目。  
  
    1.  **（找不到資料庫）**是停用，隨時都呈現灰色  
  
    2.  **建立新的資料庫**這在只有當 Azure SQL DB 帳戶上沒有資料庫時，才會啟用。 按一下這個功能表項目，建立 Azure 資料庫 對話方塊才會出現在資料庫的名稱和大小。  
  
3.  在建立資料庫時，下列兩個參數提供做為輸入：  
  
    1.  **資料庫名稱：**輸入資料庫名稱。  
  
    2.  **資料庫大小：**選取您要在 Azure SQL DB 帳戶中建立的資料庫大小。  
  

