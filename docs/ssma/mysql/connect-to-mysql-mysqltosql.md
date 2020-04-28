---
title: 連接到 MySQL （MySQLToSQL） |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 94099d01-ab19-4d58-a172-340c86b4a0f3
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 3fe4b59a5131838357d7f58e5333e0ba6b9c80f2
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68103236"
---
# <a name="connect-to-mysql-mysqltosql"></a>連線到 MySQL (MySQLToSQL)
使用 [**連接到 mysql** ] 對話方塊，即可連線到您想要遷移的 MySQL 資料庫。  
  
若要存取此對話方塊，請在 [檔案]**功能表上，選取 [連線****到 MySQL]**。 如果您先前已連線，此命令會**重新連接到 MySQL**。  
  
## <a name="options"></a>選項  
**提供者**  
  
可用的 MySQL 提供者為 MySQL ODBC 5.1 驅動程式（受信任）。  
  
**Mode**  
  
預設模式為 [標準] 模式。 在標準模式中，您可以輸入或選取 MySQL、伺服器名稱、伺服器埠、使用者名稱和密碼的值。  
  
**伺服器名稱**  
  
輸入 MySQL 伺服器名稱。 這是標準模式選項。  
  
**伺服器通訊埠**  
  
輸入伺服器埠。 預設的伺服器埠是3306。 這是標準模式選項。  
  
**使用者名稱**  
  
輸入 SSMA 將用來連接到 MySQL 資料庫的使用者名稱。  
  
**密碼**  
  
請輸入使用者名稱的密碼。  
  
**SSL**  
  
如果您想要安全地連線到 MySQL，請核取 [ **SSL** ] 核取方塊，以使用安全通訊端層（ssl）。  
  
**設定**  
  
它提供選項來設定透過安全通訊端層（SSL）的 MySQL 連線。  
  
> [!NOTE]  
> 若要**啟用 [設定]**，SSL 必須設定為 [ **True**]。  
  
當您按一下 [設定] 按鈕時，就會出現對話方塊。 若要在連接到 MySQL 資料庫時使用加密，必須定義對話方塊中的下列三個憑證檔案的路徑 [隱私權增強郵件憑證（PEM）]：  
  
-   **SSL 憑證頒發機構單位：** 指定具有信任 SSL Ca 清單之檔案的路徑。  
  
-   **SSL 憑證：** 指定要用來建立安全連線的 SSL 憑證檔案名。  
  
-   **SSL 金鑰：** 指定要用來建立安全連線的 SSL 金鑰檔名稱。  
  
> [!NOTE]  
> -   提供必要的資訊時，會啟用 [**確定]** 按鈕。 如果有任何檔案路徑無效，[確定] 按鈕將會保持停用狀態。  
> -   [**取消**] 按鈕會關閉對話方塊，並從主要連接窗**體關閉 [** SSL] 選項。  
  
