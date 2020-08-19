---
description: '連接至 Azure SQL Database (AccessToSQL) '
title: 連接至 Azure SQL Database (AccessToSQL) |Microsoft Docs
ms.prod: sql
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Connect to SQL Azure dialog box
ms.assetid: bf44b236-d9be-41ae-a5fd-bd73038e505f
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 15882852544113881b52f3641e0c85ec684add22
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88418564"
---
# <a name="connect-to-azure-sql-database-accesstosql"></a>連接至 Azure SQL Database (AccessToSQL) 
使用 [連接到 SQL Azure] 對話方塊，即可連接到您想要遷移 Azure SQL Database 中的資料庫。  
  
若要存取此對話方塊， **請在 [** 檔案] 功能表上選取 **[連接到 SQL Azure]**。 如果您先前已連線，命令會 **重新連接至 SQL Azure。**  
  
## <a name="options"></a>選項。  
**伺服器名稱**  
  
選取或輸入伺服器名稱，以連接至 SQL Azure。  
  
**Database**  
  
選取，輸入或 **流覽** 資料庫名稱。  
  
> [!IMPORTANT]  
> SSMA for Access 不支援連接到 SQL Azure 中的 master 資料庫。  
  
**使用者名稱**  
  
輸入 SSMA 將用來連接的使用者名稱 Azure SQL Database  
  
**密碼**  
  
請輸入使用者名稱的密碼。  
  
**Encrypt**  
  
SSMA 建議對 SQL Azure 進行加密的連接。  
  
## <a name="create-database"></a>建立資料庫  
若要建立新的資料庫，請遵循下列步驟  
  
1.  按一下出現在 [連接到 SQL Azure] 對話方塊中的 [流覽] 按鈕  
  
2.  如果沒有資料庫，則會出現兩個功能表項目  
  
    1.  ** (找不到任何資料庫) ** 已停用，而且所有時間都變成灰色  
  
    2.  建立永遠啟用的**新資料庫**，讓使用者能夠建立新的資料庫。 當您按一下這個功能表項目時，[建立資料庫] 對話方塊就會出現，並顯示資料庫名稱和大小。  
  
3.  建立資料庫時，會將這兩個參數指定為輸入。  
  
    1.  **資料庫名稱：** 輸入資料庫名稱。  
  
    2.  **資料庫大小：** 選取您需要在 SQL Azure 帳戶中建立的資料庫大小。  
  
