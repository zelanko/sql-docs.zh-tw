---
description: 第 2 課：設定資料庫物件的權限
title: 教學課程：設定資料庫物件的權限
ms.custom: seo-lt-2019
ms.date: 07/31/2018
ms.prod: sql
ms.technology: t-sql
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- database permissions
ms.assetid: f964b66a-ec32-44c2-a185-6a0f173bfa22
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e254a0f99ed717dbfde73f671d905ce8ecdf8264
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97465999"
---
# <a name="lesson-2-configure-permissions-on-database-objects"></a>第 2 課：設定資料庫物件的權限
[!INCLUDE[tsql-appliesto-ss2008-all-md](../includes/tsql-appliesto-ss2008-all-md.md)]
授與使用者存取資料庫的權限包括三個步驟。 首先，請建立登入。 登入可讓使用者連接到 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]。 接著，請將登入設定為指定之資料庫的使用者。 最後，請授與該使用者存取資料庫物件的權限。 這一課會示範這三個步驟，並且說明如何將檢視和預存程序建立為物件。  

  >[!NOTE]
  > 本課程會用到在[課程 1 - 建立資料庫物件](lesson-1-creating-database-objects.md)中建立的物件。 在繼續課程 2 之前，請先完成課程 1。 

## <a name="prerequisites"></a>必要條件
若要完成本教學課程，您需要 SQL Server Management Studio 和 SQL Server 執行個體存取權。 

- 安裝 [SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md)。

若您沒有 SQL Server 執行個體存取權，請從下列連結選取您的平台。 若您選擇 SQL 驗證，請使用您的 SQL Server 登入認證。
- **Windows**: [下載 SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads).
- **macOS**: [下載 Docker 上的 SQL Server 2017](../linux/quickstart-install-connect-docker.md).

[!INCLUDE[Freshness](../includes/paragraph-content/fresh-note-steps-feedback.md)]

## <a name="create-a-login"></a>建立登入
若要存取 [!INCLUDE[ssDE](../includes/ssde-md.md)]，使用者需要登入。 登入可以用 Windows 帳戶或 Windows 群組的成員來代表使用者的身分識別，或者登入也可以是只存在於 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]登入。 請盡可能使用「Windows 驗證」。  
  
依預設，電腦的管理員具有 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的完整存取權。 在這一課中，我們希望有權限較低的使用者，因此您將會在電腦上建立新的本機「Windows 驗證」帳戶。 若要執行此作業，您必須是電腦的管理員。 接著，您將會為新使用者授與 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的存取權。  
  
### <a name="create-a-new-windows-account"></a>建立新的 Windows 帳戶  
  
1.  依序按一下 [開始] 和 [執行]，在 [開啟] 方塊中輸入 **%SystemRoot%\system32\compmgmt.msc /s**，然後按一下 [確定] 開啟 [電腦管理] 程式。 
2.  在 [系統工具] 底下，展開 [本機使用者和群組]，以滑鼠右鍵按一下 [使用者]，然後按一下 [新增使用者]。    
3.  在 [使用者名稱] 方塊中輸入 **Mary**。    
4.  在 [密碼] 和 [確認密碼] 方塊中輸入強式密碼，然後按一下 [建立]，建立新的本機 Windows 使用者。  
  
### <a name="create-a-sql-login"></a>建立 SQL 登入  

在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]的 [查詢編輯器] 視窗中，輸入並執行下列程式碼，並以您的電腦名稱取代 `computer_name` 。 `FROM WINDOWS` 表示 Windows 將會驗證使用者。 選擇性的 `DEFAULT_DATABASE` 引數會將 `Mary` 連接到 `TestData` 資料庫，除非她的連接字串指定要連接到其他資料庫。 這個陳述式採用分號作為 [!INCLUDE[tsql](../includes/tsql-md.md)] 陳述式的選擇性結束符號。
  
  ```sql  
  CREATE LOGIN [computer_name\Mary]  
      FROM WINDOWS  
      WITH DEFAULT_DATABASE = [TestData];  
  GO  
  ```  
  
  這個陳述式會授權使用者名稱 `Mary`在經過電腦驗證之後，可以存取這個 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]執行個體。 如果電腦上有一個以上的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體，則您必須在 `Mary` 需要存取的每一個執行個體上分別建立登入。    
  > [!NOTE]  
  > 由於 `Mary` 不是網域帳戶，因此這個使用者名稱只能在這部電腦上進行驗證。 


## <a name="grant-access-to-a-database"></a>授與資料庫的存取權
Mary 現在已具有此 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]執行個體的存取權，但是沒有存取資料庫的權限。 必須等到您將她授權為資料庫使用者之後，她才能存取預設的 **TestData** 資料庫。  
  
若要授與 Mary 存取權，請切換到 **TestData** 資料庫，然後使用 CREATE USER 陳述式將其登入對應至名為 Mary 的使用者。  
  
### <a name="to-create-a-user-in-a-database"></a>若要在資料庫中建立使用者  
  
輸入並執行下列陳述式 (以您的電腦名稱取代 `computer_name` )，為 `Mary` 授與 `TestData` 資料庫的存取權。
  
 ```sql  
 USE [TestData];  
 GO  
 
 CREATE USER [Mary] FOR LOGIN [computer_name\Mary];  
 GO    
 ```  
  
 現在 Mary 即具有 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 和 `TestData` 資料庫兩者的存取權。  


## <a name="create-views-and-stored-procedures"></a>建立檢視和預存程序
 作為管理員，您可以從 **Products** 資料表和 **vw_Names** 檢視中執行 SELECT，也可以執行 **pr_Names** 預存程序；但 Mary 則無權這麼做。 若要授與 Mary 必要的權限，請使用 GRANT 陳述式。  

### <a name="grant-permission-to-stored-procedure"></a>將權限授與預存程序  
執行下列陳述式，讓 `Mary` 具有 `EXECUTE` 預存程序的 `pr_Names` 權限。
  
  ```sql  
  GRANT EXECUTE ON pr_Names TO Mary;  
  GO  
  ```  
  
在這個狀況中，Mary 只能使用預存程序來存取 **Products** 資料表。 如果您希望 Mary 能夠在檢視中執行 SELECT 陳述式，則必須也要執行 `GRANT SELECT ON vw_Names TO Mary`。 若要移除資料庫物件的存取權，請使用 REVOKE 陳述式。  
  
> [!NOTE]  
> 如果資料表、檢視和預存程序並不是由相同的結構描述所擁有，則授與權限的過程將會更加複雜。  
  
### <a name="about-grant"></a>關於 GRANT  
您必須具有 EXECUTE 權限，才能執行預存程序。 若要存取和變更資料，則必須具有 SELECT、INSERT、UPDATE 和 DELETE 權限。 GRANT 陳述式也可以用來授與其他權限，例如建立資料表的權限。  
  
## <a name="next-steps"></a>接下來的步驟
下一篇文章會教您如何移除您在其他課程中建立的資料庫物件。 

請前往下一篇文章以深入了解：
> [!div class="nextstepaction"]
>[後續步驟](lesson-3-deleting-database-objects.md)
