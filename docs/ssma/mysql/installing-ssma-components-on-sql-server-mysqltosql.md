---
title: 在 SQL Server (MySQLToSql) 上安裝 SSMA 元件 |Microsoft Docs
description: 在執行 SQL Server 的伺服器上安裝元件，以支援使用 SSMA 的 MySQL 資料庫轉換，包括 SSMA 延伸模組套件和 MySQL 提供者。
ms.prod: sql
ms.custom: ''
ms.date: 07/14/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- SSMA extension pack, Installation
ms.assetid: 6772d0c5-258f-4d7b-afb0-b5f810e71af1
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: a38808c64209edb094c986e63305707a0a834edb
ms.sourcegitcommit: 777704aefa7e574f4b7d62ad2a4c1b10ca1731ff
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/06/2020
ms.locfileid: "87823664"
---
# <a name="installing-ssma-components-on-sql-server-mysqltosql"></a>在 SQL Server (MySQLToSql 上安裝 SSMA 元件) 

除了安裝 SSMA 以外，您也必須在執行的電腦上安裝元件 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 這些元件包括支援資料移轉的 SSMA 延伸模組套件，以及可啟用伺服器對伺服器連線能力的 MySQL 提供者。

## <a name="ssma-for-mysql-extension-pack"></a>適用于 MySQL 的 SSMA 擴充功能套件

SSMA 延伸模組套件會將資料庫**sysdb**加入至指定的實例 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 這個資料庫包含遷移資料所需的資料表和預存程式。

此外，當您將資料移轉至時 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，SSMA [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會在伺服器端資料移轉引擎用於遷移資料時，建立 Agent 作業。

### <a name="prerequisites"></a>必要條件

在上安裝 SSMA for MySQL 伺服器元件之前 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，請確定電腦符合下列需求：

- [!INCLUDE[msCoName](../../includes/msconame_md.md)]Windows Installer 3.1 或更新版本。
- [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] 版本4.7.2 或更新版本。 您可以從[.NET Framework 開發人員中心](https://go.microsoft.com/fwlink/?LinkId=48882)取得此檔案。
- MySQL 用戶端提供者，以及您要遷移之 MySQL 資料庫的連線能力。 您可以從 MySQL 產品媒體或 MySQL 網站安裝提供者。
- 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝期間，Browser 服務必須正在執行。 這是用來 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在安裝精靈中填入實例的清單。 您可以在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝後停用 Browser 服務。  

  > [!NOTE]
  > 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服務正在執行，但您仍然看不到安裝程式中的實例清單，則必須解除封鎖 UDP 埠1434。 您可以使用 Windows 防火牆暫時解除封鎖通訊埠，也可以暫時停用 Windows 防火牆。 您也可能需要暫時停用防毒軟體。 請務必在安裝後啟用防火牆和防毒軟體。

### <a name="installing-the-extension-pack"></a>安裝延伸模組套件

您可以在將資料移轉至之前，隨時安裝延伸模組套件 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。

> [!IMPORTANT]
> 若要安裝延伸模組套件，您必須是實例上**系統管理員（sysadmin** ）伺服器角色的成員 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。

若要安裝延伸模組套件：

1. 將**SSMAforMySQLExtensionPack_*n*.msi**的 SSMA （其中*n*是組建編號）複製到執行的電腦 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。
2. 按兩下 [ **SSMAforMySQLExtensionPack_*n*.msi**]。
3. 在 [**歡迎使用**] 對話方塊中，按 **[下一步**]。
4. 在 [**使用者授權合約**] 對話方塊中，閱讀授權合約。 如果您同意，請選取 [**我接受合約**] 選項，然後按 **[下一步]**。
5. 在 [**選擇安裝類型**] 對話方塊上，按一下 [**一般**]。
6. 在 [**準備安裝**] 對話方塊中，按一下 [**安裝**]。
7. 在 [**完成安裝的第一個步驟**] 對話方塊中，按 **[下一步]**。

   此時會出現新的對話方塊，您可以在其中選取擴充功能 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 套件安裝的實例。
  
8. 選取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 您將在其中遷移 MySQL 架構的實例，然後按 **[下一步]**。
  
   預設實例與電腦具有相同的名稱。 命名實例後面會接著一個反斜線和實例名稱。

9. 在 [連接] 頁面上，選取驗證方法，然後按 **[下一步]**。
  
    Windows 驗證會使用您的 Windows 認證來嘗試登入的實例 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 如果您選取 [伺服器驗證]，則必須輸入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入名稱和密碼。

10. 接下來，您必須設定主要金鑰的密碼，以便在伺服器端資料移轉期間，用來加密儲存在延伸模組套件資料庫中的任何敏感性資料。 提供強式密碼，然後按 **[下一步]**。

11. 在下一個對話方塊中，選取 [**安裝公用*n*程式資料庫] 並安裝延伸模組套件程式庫**（其中*n*是版本號碼），然後按 **[下一步]**。

    **Sysdb**資料庫是以資料移轉所需的資料表和預存程式來建立， (使用伺服器端資料移轉引擎) 會在此資料庫中建立。

12. 若要將公用程式安裝到另一個實例 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，請選取 **[是]**，然後按 **[下一步]**。 或者，若要結束嚮導，請按一下 [**否**]。

## <a name="see-also"></a>另請參閱

- [安裝 SSMA for MySQL 用戶端](../../ssma/mysql/installing-ssma-for-mysql-client-mysqltosql.md)
- [將 MySQL 資料庫遷移至 SQL Server Azure SQL Database](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)
