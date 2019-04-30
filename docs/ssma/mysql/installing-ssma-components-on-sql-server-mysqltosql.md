---
title: SQL Server (MySQLToSql) 上安裝 SSMA 元件 |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 1f80198787dd85d8f0c65e9881925641f9f081e5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63233046"
---
# <a name="installing-ssma-components-on-sql-server-mysqltosql"></a>在 SQL Server 上安裝 SSMA 元件 (MySQLToSql)
除了安裝 SSMA，您必須也安裝元件正在執行的電腦上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 這些元件包括 SSMA 延伸模組套件，可支援資料移轉和 MySQL 提供者，以啟用伺服器對伺服器連線。  
  
## <a name="ssma-for-mysql-extension-pack"></a>SSMA for MySQL 擴充功能套件  
SSMA 延伸模組組件會加入資料庫中， **sysdb**，以指定的執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 此資料庫包含的資料表和資料移轉所需的預存程序。  
  
此外，當您將資料移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，建立 SSMA[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理程式作業，會使用伺服器端資料移轉引擎來移轉資料時。  
  
### <a name="prerequisites"></a>先決條件  
您在上安裝 SSMA for MySQL 伺服器元件之前[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，請確定電腦是否符合下列需求：  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows Installer 3.1 或更新版本。  
  
-   MySQL 用戶端提供者，並連線至您想要移轉的 MySQL 資料庫中。 您可以從 MySQL 產品媒體或 MySQL 網站上安裝提供者。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服務必須在安裝期間執行。 這用來填入清單的執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]在安裝精靈。 您可以停用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]之後安裝的瀏覽器服務。  
  
    > [!NOTE]  
    > 如果[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]瀏覽器服務正在執行，但您仍然看不見安裝程式中的執行個體的清單，您必須解除封鎖 UDP 通訊埠 1434年。 您可以使用 Windows 防火牆來暫時解除封鎖連接埠，或您可以暫時停用 Windows 防火牆。 您也可能會暫時停用防毒軟體。 請務必在安裝之後，啟用防火牆和防毒軟體。  
  
### <a name="installing-the-extension-pack"></a>安裝延伸模組組件  
您可以安裝的延伸模組組件之前您將資料移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
> [!IMPORTANT]  
> 若要安裝的延伸模組組件，您必須隸屬**sysadmin**伺服器角色的執行個體上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
**若要安裝的延伸模組組件**  
  
1.  複製 SSMA for MySQL 擴充功能套件。*n*。Install.exe，其中*n*是組建編號，來執行電腦[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
2.  按兩下 SSMA for MySQL 擴充功能套件。*n*。Install.exe。  
  
3.  在 [歡迎使用] 對話方塊中，按一下 [**下一步]**。  
  
4.  在 [使用者授權合約] 對話方塊中，閱讀授權合約。 如果您同意，請選取**我接受授權合約中的條款**核取方塊，然後按一下**下一步**。  
  
5.  在 選擇安裝類型 對話方塊中，按一下 **典型**。  
  
6.  在 [準備安裝] 對話方塊中，按一下**安裝**。  
  
7.  在 [已完成安裝的第一個步驟] 對話方塊中，按一下 [**下一步]**。  
  
    新的對話方塊隨即出現，您可以在其中選取執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]延伸模組套件安裝。  
  
8.  選取的執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，您將會移轉 MySQL 結構描述，然後按一下**下一步**。  
  
    預設執行個體具有相同名稱的電腦。 具名執行個體將加上反斜線與執行個體名稱。  
  
9. 在 [連線] 對話方塊中，選取驗證方法，然後按一下 [**下一步]**。  
  
    Windows 驗證將用來嘗試登入的執行個體的 Windows 認證[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如果您選取[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證，您必須輸入[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登入名稱和密碼。  
  
10. 在下一步 對話方塊中，選取**安裝公用程式資料庫** *n*，其中*n*是版本號碼，然後按一下**下一步**。  
  
    **Sysdb**資料庫建立的資料表和資料移轉 （使用伺服器端資料移轉引擎） 所需的預存程序會建立該資料庫中。  
  
11. 若要安裝的另一個執行個體的公用程式[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，選取 **[是]**，然後按一下**下一步**。 或者，若要結束精靈，請按一下**No**。  
  
## <a name="see-also"></a>另請參閱  
[安裝 SSMA for MySQL 用戶端&#40;MySQLToSQL&#41;](../../ssma/mysql/installing-ssma-for-mysql-client-mysqltosql.md)  
[移轉 MySQL 資料庫到 SQL Server-Azure SQL DB &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
