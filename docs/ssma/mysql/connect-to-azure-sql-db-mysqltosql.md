---
description: '連接至 Azure SQL Database (MySQLToSQL) '
title: 連接至 Azure SQL Database (MySQLToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 81623d27-25af-444f-9779-1edb8c6fb470
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: cf3112f6b431fae9149df76464ed576f89a51dd1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88454130"
---
# <a name="connect-to-azure-sql-database-mysqltosql"></a>連接至 Azure SQL Database (MySQLToSQL) 
使用 [連接到 SQL Azure] 對話方塊，即可連接到您想要遷移 Azure SQL Database 中的資料庫。  
  
若要存取此對話方塊， **請在 [** 檔案] 功能表上選取 **[連接到 SQL Azure]**。 如果您先前已連線，命令會 **重新連接至 SQL Azure。**  
  
## <a name="options"></a>選項。  
**伺服器名稱**  
  
選取或輸入伺服器名稱，以連接至 SQL Azure。  
  
**Database**  
  
選取，輸入或 **流覽** 資料庫名稱。  
  
> [!IMPORTANT]  
> 適用于 MySQL 的 SSMA 不支援連接至 SQL Azure 中的 master 資料庫。  
  
**使用者名稱**  
  
輸入 SSMA 將用來連接的使用者名稱 Azure SQL Database  
  
**密碼**  
  
請輸入使用者名稱的密碼。  
  
**Encrypt**  
  
SSMA 建議對 SQL Azure 進行加密的連接。  
  
## <a name="create-azure-database"></a>建立 Azure 資料庫  
如果 SQL Azure 帳戶中沒有任何資料庫，您可以建立第一個資料庫。  
  
若要在第一次建立新的資料庫，請遵循下列步驟  
  
1.  按一下出現在 [連接到 SQL Azure] 對話方塊中的 [流覽] 按鈕  
  
2.  如果沒有資料庫，則會出現下列兩個功能表項目。  
  
    1.  ** (找不到任何資料庫) ** 已停用，而且所有時間都變成灰色  
  
    2.  **建立新的資料庫** ，只有在 SQL Azure 帳戶上沒有任何資料庫時才會啟用。 當您按一下此功能表項目時，[建立 Azure 資料庫] 對話方塊會存在於資料庫名稱和大小。  
  
3.  建立資料庫時，會將下列兩個參數指定為輸入：  
  
    1.  **資料庫名稱：** 輸入資料庫名稱。  
  
    2.  **資料庫大小：** 選取您需要在 SQL Azure 帳戶中建立的資料庫大小。  
  
