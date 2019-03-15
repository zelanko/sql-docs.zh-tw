---
title: RevoScaleR 教學課程-SQL Server Machine Learning 中建立資料庫和權限
description: 有關如何建立 R 教學課程適用於 SQL Server 資料庫的教學課程逐步解說...
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: af64387490de8af43d29742e7b388ab1755896b7
ms.sourcegitcommit: e9fcd10c7eb87a4f09ac2d8f7647018e83a5f5c5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/14/2019
ms.locfileid: "57976338"
---
# <a name="create-a-database-and-permissions-sql-server-and-revoscaler-tutorial"></a>建立資料庫和權限 （SQL Server 和 RevoScaleR 教學課程）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

這一課是屬於[RevoScaleR 教學課程](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)如何使用[RevoScaleR 函數](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)與 SQL Server。

其中一個的課程是有關設定 SQL Server 資料庫和權限才能完成本教學課程。 使用[SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)或另一個查詢編輯器，來完成下列工作：

> [!div class="checklist"]
> * 建立新的資料庫來儲存資料以供訓練和評分兩個 R 模型
> * 建立資料庫使用者登入以建立和使用資料庫物件的權限
  
## <a name="create-the-database"></a>建立資料庫

本教學課程需要資料庫來儲存資料和程式碼。 如果您不是系統管理員，要求您為您建立的資料庫和登入的 DBA。 您需要的權限來寫入和讀取資料，以及執行 R 指令碼。

1. 在 SQL Server Management Studio 中，連接到 R 啟用資料庫執行個體。

2. 以滑鼠右鍵按一下**資料庫**，然後選取**新的資料庫**。
  
2. 輸入新資料庫的名稱：RevoDeepDive。
  

## <a name="create-a-login"></a>建立登入
  
1. 將資料庫內容變更為 master 資料庫並按一下 [新增查詢]。
  
2. 在新的 [查詢] 視窗中，執行下列命令以建立使用者帳戶，並將帳戶指派給此教學課程中所用的資料庫。 請務必視需要變更資料庫名稱。

3. 若要確認登入，請選取新的資料庫，展開**安全性**，展開**使用者**。
  
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

本教學課程會示範 R 指令碼和 DDL 作業，包括建立和刪除資料表和預存程序，以及在外部處理序中執行 R 指令碼，在 SQL Server 上。 在此步驟中，指派權限以允許這些工作。

這個範例假設 SQL 登入 (DDUser01)，但如果您建立的 Windows 登入，可改為使用。

```sql
USE RevoDeepDive
GO

EXEC sp_addrolemember 'db_owner', 'DDUser01'
GRANT EXECUTE ANY EXTERNAL SCRIPT TO DDUser01
GO
```

## <a name="troubleshoot-connections"></a>針對連線進行疑難排解

本節列出在資料庫設定過程中可能發生的一些常見問題。

- **如何確認資料庫連線和檢查 SQL 查詢？**
  
    在使用伺服器執行 R 程式碼之前，您可能想檢查資料庫是否能與 R 開發環境連線。 [Visual Studio 中的伺服器總管](https://docs.microsoft.com/previous-versions/x603htbk(v=vs.140)) 和 [SQL Server Management Studio](../../ssms/download-sql-server-management-studio-ssms.md) 都是免費工具，具有功能強大的資料庫連線和管理功能。
  
    如果您不想安裝其他資料庫管理工具，可以使用控制台的 [ODBC 資料來源管理員](https://docs.microsoft.com/sql/odbc/admin/odbc-data-source-administrator?view=sql-server-2017) ，建立與 SQL Server 執行個體的測試連線。 如果資料庫已正確設定且輸入的使用者名稱和密碼皆無誤時，您應可看到剛建立的資料庫，並可將其選取為預設資料庫。
  
    連接失敗的常見原因包括遠端伺服器時，不會啟用連接，而且未啟用具名管道通訊協定。 您可以在這篇文章中找到更多的疑難排解秘訣：[疑難排解 SQL Server Database Engine 的連接](https://docs.microsoft.com/sql/database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine)。
  
- **為什麼我的資料表名稱前會加上資料讀取元？**
  
    當您指定做為這位使用者的預設結構描述**db_datareader**，所有資料表和其他新的物件，此使用者建立的前面會加上*結構描述*名稱。 結構描述就像是一個資料夾，您可以新增到資料庫以便組織物件。 結構描述也可定義資料庫內的使用者權限。
  
    與一個特定的使用者名稱相關聯的結構描述時，使用者是_結構描述擁有者_。 在建立物件時，除非您特別要求要以另一個結構描述來建立，否則一律會以您自己的結構描述來建立物件。
  
    例如，如果您建立的資料表名稱**TestData**，且您的預設結構描述**db_datareader**，資料表會建立具有名稱`<database_name>.db_datareader.TestData`。
  
    因此，資料庫可以包含多個具有相同名稱的資料表，只要資料表屬於不同的結構描述即可。
   
    如果您要尋找資料表，但不指定結構描述，資料庫伺服器會尋找您所擁有的結構描述。 因此，如果資料表含有與您的登入相關聯的結構描述，存取這類資料表時就不需要指定結構描述名稱。
  
- **我沒有 DDL 權限，是否仍可以執行本教學課程？**
  
    是的但您應該先請使用者預先載入資料至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料表，以及略過 繼續進行下一課。 需要 DDL 權限的函式會反映在本教學課程可能的情況下。

    此外，要求您的系統管理員授與您的權限 EXECUTE ANY EXTERNAL SCRIPT。 遠端，還是使用，執行 R 指令碼，為所需`sp_execute_external_script`。

## <a name="next-steps"></a>後續步驟

> [!div class="nextstepaction"]
> [使用 RxSqlServerData 建立 SQL Server 資料物件](../../advanced-analytics/tutorials/deepdive-create-sql-server-data-objects-using-rxsqlserverdata.md)