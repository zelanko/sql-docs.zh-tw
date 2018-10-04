---
title: 連線到 MySQL (MySQLToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 94099d01-ab19-4d58-a172-340c86b4a0f3
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 2a68b60a954e6cd89698d4e906f8272f08d6b11e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47673156"
---
# <a name="connect-to-mysql-mysqltosql"></a>連線到 MySQL (MySQLToSQL)
使用**連接到 MySQL**對話方塊，即可連接至您想要移轉的 MySQL 資料庫。  
  
若要存取此對話方塊中，在**檔案**功能表上，選取**連線到 MySQL**。 如果您先前曾經連線，則命令是**重新連接至 MySQL**。  
  
## <a name="options"></a>選項。  
**提供者**  
  
可用的 MySQL 提供者是 MySQL ODBC 5.1 驅動程式 （受信任）。  
  
**模式**  
  
預設模式為標準模式。 在標準模式中，您輸入或選取 MySQL、 伺服器名稱、 伺服器連接埠、 使用者名稱和密碼的值。  
  
**伺服器名稱**  
  
輸入 MySQL 伺服器名稱。 這是標準模式的選項。  
  
**伺服器通訊埠**  
  
輸入伺服器連接埠。 預設的伺服器連接埠為 3306。 這是標準模式的選項。  
  
**使用者名稱**  
  
輸入使用者名稱 SSMA 會將用來連接到 MySQL 資料庫。  
  
**密碼**  
  
請輸入使用者名稱的密碼。  
  
**SSL**  
  
如果您想要安全地連線至 MySQL，請使用的安全通訊端層 (SSL)，藉由檢查**SSL**核取方塊。  
  
**設定**  
  
它提供一個選項來設定 MySQL 透過安全通訊端層 (SSL) 連線。  
  
> [!NOTE]  
> 若要啟用**設定**，必須將 SSL **，則為 True**。  
  
按一下 [設定] 按鈕，對話方塊隨即出現。 若要使用加密，而連線至 MySQL 資料庫，以顯示在對話方塊中的下列三個憑證檔案的路徑必須被定義 [隱私權增強式郵件憑證 (PEM)]:  
  
-   **SSL 憑證授權單位：** 一份信任 SSL Ca 的指定檔案的路徑。  
  
-   **SSL 憑證：** 指定要用來建立安全連線的 SSL 憑證檔案的名稱。  
  
-   **SSL 金鑰：** 指定要用來建立安全連線的 SSL 金鑰檔案的名稱。  
  
> [!NOTE]  
> -   **確定**已提供所需的資訊時，已啟用 按鈕。 如果任一檔案路徑無效，則會維持停用 [確定] 按鈕。  
> -   **取消** 按鈕關閉對話方塊並**關閉**SSL 選項，從主要的連接形式。  
  
