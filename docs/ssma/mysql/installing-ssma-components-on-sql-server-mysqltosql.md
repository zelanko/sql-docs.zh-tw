---
title: 在 SQL Server 上安裝 SSMA 元件（MySQLToSql） |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- SSMA extension pack, Installation
ms.assetid: 6772d0c5-258f-4d7b-afb0-b5f810e71af1
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 64040f4a0caf8253e6d6e8a3b00ff21e0cebe6d9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68075353"
---
# <a name="installing-ssma-components-on-sql-server-mysqltosql"></a>在 SQL Server 上安裝 SSMA 元件 (MySQLToSql)
除了安裝 SSMA 以外，您也必須在執行的電腦上安裝元件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 這些元件包括支援資料移轉的 SSMA 延伸模組套件，以及可啟用伺服器對伺服器連線能力的 MySQL 提供者。  
  
## <a name="ssma-for-mysql-extension-pack"></a>適用于 MySQL 的 SSMA 擴充功能套件  
SSMA 延伸模組套件會將資料庫**sysdb**加入至指定的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]實例。 這個資料庫包含遷移資料所需的資料表和預存程式。  
  
此外，當您將資料移轉[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]至時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SSMA 會在伺服器端資料移轉引擎用於遷移資料時，建立 Agent 作業。  
  
### <a name="prerequisites"></a>Prerequisites  
在上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安裝 SSMA for MySQL 伺服器元件之前，請確定電腦符合下列需求：  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)]Windows Installer 3.1 或更新版本。  
  
-   MySQL 用戶端提供者，以及您要遷移之 MySQL 資料庫的連線能力。 您可以從 MySQL 產品媒體或 MySQL 網站安裝提供者。  
  
-   在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安裝期間，Browser 服務必須正在執行。 這是用來在安裝精靈中填入實例的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]清單。 您可以在安裝[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]後停用 Browser 服務。  
  
    > [!NOTE]  
    > 如果[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服務正在執行，但您仍然看不到安裝程式中的實例清單，則必須解除封鎖 UDP 埠1434。 您可以使用 Windows 防火牆暫時解除封鎖通訊埠，也可以暫時停用 Windows 防火牆。 您也可能需要暫時停用防毒軟體。 請務必在安裝後啟用防火牆和防毒軟體。  
  
### <a name="installing-the-extension-pack"></a>安裝延伸模組套件  
您可以在將資料移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]之前，隨時安裝延伸模組套件。  
  
> [!IMPORTANT]  
> 若要安裝延伸模組套件，您必須是實例上**系統管理員（sysadmin** ）伺服器角色的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]成員。  
  
**安裝延伸模組套件**  
  
1.  複製 SSMA for MySQL 延伸模組套件。*n*。在執行的電腦上安裝 .exe，其中*n*是組建編號[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
2.  按兩下 [適用于 MySQL 的 SSMA 擴充功能套件]。*n*。安裝 .exe。  
  
3.  在 [歡迎使用] 對話方塊中，按 **[下一步**]。  
  
4.  在 [使用者授權合約] 對話方塊中，閱讀授權合約。 如果您同意，請選取 [**我接受授權合約中的條款**] 核取方塊，然後按 **[下一步]**。  
  
5.  在 [選擇安裝類型] 對話方塊上，按一下 [**一般**]。  
  
6.  在 [準備安裝] 對話方塊中，按一下 [**安裝**]。  
  
7.  在 [完成安裝的第一個步驟] 對話方塊中，按 **[下一步]**。  
  
    此時會出現新的對話方塊，您可以在其中選取擴充功能[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]套件安裝的實例。  
  
8.  選取您將在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]其中遷移 MySQL 架構的實例，然後按 **[下一步]**。  
  
    預設實例與電腦具有相同的名稱。 命名實例後面會接著一個反斜線和實例名稱。  
  
9. 在 [連接] 對話方塊中，選取驗證方法，然後按 **[下一步]**。  
  
    Windows 驗證會使用您的 Windows 認證來嘗試登入的實例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如果您選取[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [驗證]，則必須輸入登入名稱和密碼。  
  
10. 在下一個對話方塊中，選取 [**安裝公用程式資料庫** *n*]，其中*n*是版本號碼，然後按 **[下一步]**。  
  
    系統會使用資料移轉所需的資料表和預存程式（使用伺服器端資料移轉引擎）來建立**sysdb**資料庫，並在該資料庫中建立。  
  
11. 若要將公用程式安裝到另[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]一個實例，請選取 **[是]**，然後按 **[下一步]**。 或者，若要結束嚮導，請按一下 [**否**]。  
  
## <a name="see-also"></a>另請參閱  
[安裝適用于 MySQL 的 SSMA 用戶端 &#40;MySQLToSQL&#41;](../../ssma/mysql/installing-ssma-for-mysql-client-mysqltosql.md)  
[將 MySQL 資料庫遷移至 SQL Server-Azure SQL DB &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
