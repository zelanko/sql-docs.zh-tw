---
title: 連接到 Azure SQL DB (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 96538007-1099-40c8-9902-edd07c5620ee
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 057a39fd393be6cce9232d787b0d110a4be2035a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47640904"
---
# <a name="connect-to-azure-sql-db--sybasetosql"></a>連線到 Azure SQL DB (SybaseToSQL)
使用 [連線到 Azure SQL DB] 對話方塊中，連接到您想要移轉的 Azure SQL DB 資料庫。  
  
若要存取此對話方塊中，在**檔案**功能表上，選取**連線到 Azure SQL DB**。 如果您先前曾經連線，則命令是**重新連接到 Azure SQL DB。**  
  
## <a name="options"></a>選項。  
**伺服器名稱**  
  
選取或輸入伺服器名稱連接到 Azure SQL DB。  
  
**[資料庫備份]**  
  
選取、 輸入或**瀏覽**資料庫名稱。  
  
> [!IMPORTANT]  
> SSMA for Sybase 不支援 Azure SQL DB 中的 master 資料庫的連接。  
  
**使用者名稱**  
  
輸入 SSMA 將用來連接到 Azure SQL DB 資料庫的使用者名稱  
  
**密碼**  
  
請輸入使用者名稱的密碼。  
  
**Encrypt**  
  
SSMA 會建議加密的連線到 Azure SQL DB。  
  
## <a name="create-azure-database"></a>建立的 Azure 資料庫  
如果 Azure SQL DB 帳戶中沒有資料庫，您可以建立第一個資料庫。  
  
若要建立第一次新的資料庫，請遵循下列步驟  
  
1.  按一下出現在 [連接到 Azure SQL DB] 對話方塊中的 [瀏覽] 按鈕  
  
2.  如果沒有資料庫，則會出現下列兩個功能表項目。  
  
    1.  **（找不到資料庫）** 其中已停用，隨時都呈現灰色  
  
    2.  **建立新的資料庫**只在 Azure SQL DB 帳戶上沒有資料庫時，才啟用。 按一下這個功能表項目，建立 Azure Database 對話方塊中會出現與資料庫名稱和大小。  
  
3.  建立資料庫時，下列兩個參數會提供做為輸入：  
  
    1.  **資料庫名稱：** 輸入資料庫名稱。  
  
    2.  **資料庫大小：** 選取您要在 Azure SQL DB 帳戶中建立的資料庫大小。  
  
