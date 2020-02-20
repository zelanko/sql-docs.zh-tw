---
title: RevoScaleR 的資料庫教學課程
description: RevoScaleR 教學課程 1：如何為 R 教學課程建立 SQL Server 資料庫。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: ae2fd2d200b6a231dd76f04556d6d221df00809f
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "74947192"
---
# <a name="create-a-database-and-permissions-sql-server-and-revoscaler-tutorial"></a>建立資料庫和權限 (SQL Server 和 RevoScaleR 教學課程)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

此教學課程是 [RevoScaleR 教學課程系列](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)的第 1 個，該系列說明如何搭配 SQL Server 使用 [RevoScaleR 函式](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) \(英文\)。

此教學課程描述如何建立 SQL Server 資料庫，並設定完成此系列中其他教學課程所需的權限。 使用 [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) 或另一個查詢編輯器來完成以下工作：

> [!div class="checklist"]
> * 建立新的資料庫來儲存資料，以定型和評分兩個 R 模型
> * 透過權限建立資料庫使用者登入，以建立並使用資料庫物件
  
## <a name="create-the-database"></a>建立資料庫

本教學課程需要資料庫來儲存資料和程式碼。 如果您不是系統管理員，請要求您的 DBA 為您建立資料庫與登入。 您將會需要寫入和讀取資料，以及執行 R 指令碼的權限。

1. 在 SQL Server Management Studio 中，連線到已啟用 R 的資料庫執行個體。

2. 以滑鼠右鍵按一下 [資料庫]  ，然後選取 [新增資料庫]  。
  
2. 輸入新資料庫的名稱：RevoDeepDive。
  
## <a name="create-a-login"></a>建立登入
  
1. 將資料庫內容變更為 master 資料庫並按一下 [新增查詢]  。
  
2. 在新的 [查詢]  視窗中，執行下列命令以建立使用者帳戶，並將帳戶指派給此教學課程中所用的資料庫。 請務必視需要變更資料庫名稱。

3. 若要確認登入，請選取新的資料庫，依序展開 [安全性]  和 [使用者]  。
  
**Windows 使用者**
  
```sql
 -- Create server user based on Windows account
USE master
GO
CREATE LOGIN [<DOMAIN>\<user_name>] FROM WINDOWS WITH DEFAULT_DATABASE=[RevoDeepDive]

 --Add the new user to tutorial database
USE [RevoDeepDive]
GO
CREATE USER [<user_name>] FOR LOGIN [<DOMAIN>\<user_name>] WITH DEFAULT_SCHEMA=[db_datareader]
```

**SQL 登入**

```sql
-- Create new SQL login
USE master
GO
CREATE LOGIN [DDUser01] WITH PASSWORD='<type password here>', CHECK_EXPIRATION=OFF, CHECK_POLICY=OFF;

-- Add the new SQL login to tutorial database
USE RevoDeepDive
GO
CREATE USER [DDUser01] FOR LOGIN [DDUser01] WITH DEFAULT_SCHEMA=[db_datareader]
```

## <a name="assign-permissions"></a>指派權限

本教學課程示範 R 指令碼和資料定義語言 (Data Definition Language) 作業，包括建立和刪除表格和儲存過程，以及在 SQL Server 的外部程序中執行 R 指令碼。 在此步驟中，指派權限以允許這些工作。

這個範例假設 SQL 登入 (DDUser01)，但如果您已建立 Windows 登入，請改為使用它。

```sql
USE RevoDeepDive
GO

EXEC sp_addrolemember 'db_owner', 'DDUser01'
GRANT EXECUTE ANY EXTERNAL SCRIPT TO DDUser01
GO
```

## <a name="troubleshoot-connections"></a>對連線進行疑難排解

本節列出在資料庫設定過程中可能發生的一些常見問題。

- **如何確認資料庫連線和檢查 SQL 查詢？**
  
    在使用伺服器執行 R 程式碼之前，您可能想檢查資料庫是否能與 R 開發環境連線。 [Visual Studio 中的伺服器總管](https://docs.microsoft.com/previous-versions/x603htbk(v=vs.140)) 和 [SQL Server Management Studio](../../ssms/download-sql-server-management-studio-ssms.md) 都是免費工具，具有功能強大的資料庫連線和管理功能。
  
    如果您不想安裝其他資料庫管理工具，可以使用控制台的 [ODBC 資料來源管理員](https://docs.microsoft.com/sql/odbc/admin/odbc-data-source-administrator?view=sql-server-2017) ，建立與 SQL Server 執行個體的測試連線。 如果資料庫已正確設定且輸入的使用者名稱和密碼皆無誤時，您應可看到剛建立的資料庫，並可將其選取為預設資料庫。
  
    連線失敗的常見原因包括伺服器未啟用遠端連線，而且未啟用具名管道通訊協定。 您可以在這篇文章找到更多疑難排解秘訣：[對 SQL Server 資料庫引擎的連線進行疑難排解](https://docs.microsoft.com/sql/database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine)。
  
- **為什麼我的資料表名稱前會加上資料讀取元？**
  
    當您將某位使用者的預設結構描述指定為 **db_datareader** 時，由該位使用者建立的所有資料表和其他新物件都會在前面加上這個*結構描述*名稱。 結構描述就像是一個資料夾，您可以新增到資料庫以便組織物件。 結構描述也可定義資料庫內的使用者權限。
  
    如果結構描述已與某個特定的使用者名稱建立關聯，則該使用者為_結構描述擁有者_。 在建立物件時，除非您特別要求要以另一個結構描述來建立，否則一律會以您自己的結構描述來建立物件。
  
    例如，如果您建立的資料表名稱為 **TestData**，而預設結構描述是 **db_datareader**，則會以名稱 `<database_name>.db_datareader.TestData` 建立資料表。
  
    因此，資料庫可以包含多個具有相同名稱的資料表，只要資料表屬於不同的結構描述即可。
   
    如果您要尋找資料表，但未指定結構描述，則資料庫伺服器會尋找您所擁有的結構描述。 因此，如果資料表含有與您的登入相關聯的結構描述，存取這類資料表時就不需要指定結構描述名稱。
  
- **我沒有 DDL 權限，是否仍可以執行本教學課程？**
  
    是，但您應該要求某人將資料預先載入至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表，然後直接跳到下一個教學課程。 在這個教學課程中，盡可能提出需要 DDL 權限的函數。

    此外，請要求您的系統管理員授與權限，並執行任何外部指定碼。 無論是遠端或使用 `sp_execute_external_script`，都需要執行 R 指令碼。

## <a name="next-steps"></a>後續步驟

> [!div class="nextstepaction"]
> [使用 RxSqlServerData 建立 SQL Server 資料物件](../../advanced-analytics/tutorials/deepdive-create-sql-server-data-objects-using-rxsqlserverdata.md)