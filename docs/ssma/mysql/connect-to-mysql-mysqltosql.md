---
title: 連接到 MySQL (MySQLToSQL) |Microsoft 文件
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-mysql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 94099d01-ab19-4d58-a172-340c86b4a0f3
caps.latest.revision: 9
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: fe6fd533d67dee44c4fa52a9391c302e8e285e87
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="connect-to-mysql-mysqltosql"></a>連接到 MySQL (MySQLToSQL)
使用**連接到 MySQL**對話方塊連接到您想要移轉的 MySQL 資料庫。  
  
若要存取此對話方塊，請在**檔案**功能表上，選取**連接到 MySQL**。 如果您之前已連線，則命令是**重新連接到 MySQL**。  
  
## <a name="options"></a>選項  
**提供者**  
  
可用的 MySQL 提供者是 MySQL ODBC 5.1 驅動程式 （信任）。  
  
**模式**  
  
預設模式為標準模式。 在標準模式中，您輸入或選取 MySQL、 伺服器名稱、 伺服器連接埠、 使用者名稱和密碼值。  
  
**伺服器名稱**  
  
輸入 MySQL 伺服器名稱。 這是標準模式選項。  
  
**伺服器通訊埠**  
  
輸入伺服器的連接埠。 預設的伺服器連接埠是 3306。 這是標準模式選項。  
  
**使用者名稱**  
  
輸入 SSMA 將用來連接到 MySQL 資料庫的使用者名稱。  
  
**密碼**  
  
請輸入使用者名稱的密碼。  
  
**SSL**  
  
如果您想要安全地連接到 MySQL，請檢查使用的安全通訊端層 (SSL) **SSL**核取方塊。  
  
**設定**  
  
它提供一個選項來設定對 MySQL 透過安全通訊端層 (SSL) 連線。  
  
> [!NOTE]  
> 若要啟用**設定**，SSL 必須設為**True**。  
  
按下按鈕 「 設定 」，對話方塊隨即出現。 若要使用加密，而連接到 MySQL 資料庫，出現在對話方塊中的下列三種憑證檔案的路徑必須被定義 [隱私權增強式郵件憑證 (PEM)]:  
  
-   **SSL 憑證授權單位：**信任 SSL Ca 的清單中指定檔案的路徑。  
  
-   **SSL 憑證：**指定要用來建立安全連線的 SSL 憑證檔案的名稱。  
  
-   **SSL 金鑰：**指定要用來建立安全連線的 SSL 金鑰檔案的名稱。  
  
> [!NOTE]  
> -   **確定**按鈕已啟用時未提供必要的資訊。 如果任一檔案路徑無效，將會維持停用 [確定] 按鈕。  
> -   **取消**按鈕關閉對話方塊和**關閉**SSL 選項，從主要的連線表單。  
  
