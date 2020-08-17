---
description: 連線到 MySQL (MySQLToSQL)
title: 連接至 MySQL (MySQLToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 94099d01-ab19-4d58-a172-340c86b4a0f3
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 399946496bbb649f84c9d539a9fe80f3f7919b31
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88372694"
---
# <a name="connect-to-mysql-mysqltosql"></a>連線到 MySQL (MySQLToSQL)
使用 [ **連接到 mysql** ] 對話方塊來連接到您想要遷移的 MySQL 資料庫。  
  
若要存取此對話方塊，請在 **[檔案** ] 功能表上選取 **[連線至 MySQL]**。 如果您先前已連線，命令會 **重新連線至 MySQL**。  
  
## <a name="options"></a>選項。  
**提供者**  
  
可用的 MySQL 提供者為 MySQL ODBC 5.1 驅動程式 (信任的) 。  
  
**Mode**  
  
預設模式為 [標準] 模式。 在 [標準] 模式中，輸入或選取 [MySQL]、[伺服器名稱]、[伺服器埠]、[使用者名稱] 和 [密碼] 的值。  
  
**伺服器名稱**  
  
輸入 MySQL 伺服器名稱。 這是標準模式選項。  
  
**伺服器埠**  
  
輸入伺服器埠。 預設伺服器埠為3306。 這是標準模式選項。  
  
**使用者名稱**  
  
輸入 SSMA 將用來連線至 MySQL 資料庫的使用者名稱。  
  
**密碼**  
  
請輸入使用者名稱的密碼。  
  
**SSL**  
  
如果您想要安全地連線至 MySQL，請勾選 [ **ssl** ] 核取方塊，以 (ssl) 使用安全通訊端層。  
  
**設定**  
  
它提供選項，可透過安全通訊端層 (SSL) 來設定 MySQL 的連線。  
  
> [!NOTE]  
> 若要啟用 **設定**，SSL 必須設定為 **True**。  
  
按一下 [設定] 按鈕時，對話方塊隨即出現。 若要在連線至 MySQL 資料庫時使用加密，必須在對話方塊中定義下列三個憑證檔案的路徑 [隱私權增強郵件憑證 (PEM) ]：  
  
-   **SSL 憑證頒發機構單位：** 指定具有信任 SSL Ca 清單之檔案的路徑。  
  
-   **SSL 憑證：** 指定要用於建立安全連線的 SSL 憑證檔案名。  
  
-   **SSL 金鑰：** 指定要用於建立安全連線的 SSL 金鑰檔名稱。  
  
> [!NOTE]  
> -   提供必要資訊後，就會啟用 [ **確定]** 按鈕。 如果有任何檔案路徑無效，[確定] 按鈕將會保持停用狀態。  
> -   [ **取消** ] 按鈕會關閉對話方塊，並從主要連接表單 **關閉** [SSL] 選項。  
  
