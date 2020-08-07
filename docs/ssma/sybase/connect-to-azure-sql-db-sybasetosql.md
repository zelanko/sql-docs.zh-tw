---
title: 連接到 Azure SQL Database (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 96538007-1099-40c8-9902-edd07c5620ee
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 02db151ff7adbc2d2595ed0eeda385c5a0367126
ms.sourcegitcommit: 21bedbae28840e2f96f5e8b08bcfc794f305c8bc
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/06/2020
ms.locfileid: "87864775"
---
# <a name="connect-to-azure-sql-database--sybasetosql"></a>連接到 Azure SQL Database (SybaseToSQL) 
使用 [連接到 Azure SQL Database] 對話方塊，即可連接到您要遷移的 Azure SQL Database 資料庫。  
  
若要存取此對話方塊，請在 **[檔案**] 功能表上，選取 [**連接到 Azure SQL Database]**。 如果您先前已連線，此命令會**重新連接到 Azure SQL Database。**  
  
## <a name="options"></a>選項。  
**伺服器名稱**  
  
選取或輸入伺服器名稱，以連接到 Azure SQL Database。  
  
**Database**  
  
選取 []，輸入或**流覽**資料庫名稱。  
  
> [!IMPORTANT]  
> SSMA for Sybase 不支援連接到 Azure SQL Database 中的 master 資料庫。  
  
**使用者名稱**  
  
輸入 SSMA 將用來連接 Azure SQL Database 資料庫的使用者名稱  
  
**密碼**  
  
請輸入使用者名稱的密碼。  
  
**Encrypt**  
  
SSMA 建議 Azure SQL Database 的加密連接。  
  
## <a name="create-azure-database"></a>建立 Azure 資料庫  
如果 Azure SQL Database 帳戶中沒有任何資料庫，您可以建立第一個資料庫。  
  
若要在第一次建立新的資料庫，請遵循下列步驟  
  
1.  按一下 [連接到 Azure SQL Database] 對話方塊中出現的 [流覽] 按鈕  
  
2.  如果沒有資料庫，則會出現下列兩個功能表項目。  
  
    1.  ** (找不到任何資料庫) **已停用且所有時間皆為灰色  
  
    2.  **建立新的資料庫**，只有在 Azure SQL Database 帳戶上沒有資料庫時才會啟用。 按一下此功能表項目時，會出現 [建立 Azure 資料庫] 對話方塊，其中包含資料庫名稱和大小。  
  
3.  在建立資料庫時，會將下列兩個參數指定為輸入：  
  
    1.  **資料庫名稱：** 輸入資料庫名稱。  
  
    2.  **資料庫大小：** 選取您需要在 Azure SQL Database 帳戶中建立的資料庫大小。  
  
