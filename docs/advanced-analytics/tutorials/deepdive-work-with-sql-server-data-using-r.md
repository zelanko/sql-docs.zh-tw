---
title: 建立 RevoScaleR 教學課程的資料庫和許可權
description: 如何為 R 教學課程建立 SQL Server 資料庫的教學課程逐步解說。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 14c07b5b2ebf30f23083921f210563bc2cb83dbf
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715537"
---
# <a name="create-a-database-and-permissions-sql-server-and-revoscaler-tutorial"></a>建立資料庫和許可權 (SQL Server 和 RevoScaleR 教學課程)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

這一課是[RevoScaleR 教學](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)課程的一部分, 說明如何搭配 SQL Server 使用[RevoScaleR 函數](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)。

第一課是關於設定 SQL Server 資料庫, 以及完成本教學課程所需的許可權。 使用[SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)或其他查詢編輯器來完成下列工作:

> [!div class="checklist"]
> * 建立新的資料庫來儲存用於定型和評分兩個 R 模型的資料
> * 建立資料庫使用者登入, 並提供建立和使用資料庫物件的許可權
  
## <a name="create-the-database"></a>建立資料庫

本教學課程需要資料庫來儲存資料和程式碼。 如果您不是系統管理員, 請要求您的 DBA 建立資料庫並登入。 您將需要有寫入和讀取資料, 以及執行 R 腳本的許可權。

1. 在 SQL Server Management Studio 中, 連接到啟用 R 的資料庫實例。

2. 以滑鼠右鍵按一下 [**資料庫**], 然後選取 [**新增資料庫**]。
  
2. 輸入新資料庫的名稱:RevoDeepDive.
  

## <a name="create-a-login"></a>建立登入
  
1. 將資料庫內容變更為 master 資料庫並按一下 [新增查詢]。
  
2. 在新的 [查詢] 視窗中，執行下列命令以建立使用者帳戶，並將帳戶指派給此教學課程中所用的資料庫。 請務必視需要變更資料庫名稱。

3. 若要確認登入, 請選取新的資料庫, 展開 [**安全性**], 然後展開 [**使用者**]。
  
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

## <a name="assign-permissions"></a>指派許可權

本教學課程示範 R 腳本和 DDL 作業, 包括建立和刪除資料表和預存程式, 以及在 SQL Server 的外部進程中執行 R 腳本。 在此步驟中, 請指派許可權以允許這些工作。

這個範例假設 SQL 登入 (DDUser01), 但如果您已建立 Windows 登入, 請改為使用它。

```sql
USE RevoDeepDive
GO

EXEC sp_addrolemember 'db_owner', 'DDUser01'
GRANT EXECUTE ANY EXTERNAL SCRIPT TO DDUser01
GO
```

## <a name="troubleshoot-connections"></a>疑難排解連接

本節列出在資料庫設定過程中可能發生的一些常見問題。

- **如何確認資料庫連線和檢查 SQL 查詢？**
  
    在使用伺服器執行 R 程式碼之前，您可能想檢查資料庫是否能與 R 開發環境連線。 [Visual Studio 中的伺服器總管](https://docs.microsoft.com/previous-versions/x603htbk(v=vs.140)) 和 [SQL Server Management Studio](../../ssms/download-sql-server-management-studio-ssms.md) 都是免費工具，具有功能強大的資料庫連線和管理功能。
  
    如果您不想安裝其他資料庫管理工具，可以使用控制台的 [ODBC 資料來源管理員](https://docs.microsoft.com/sql/odbc/admin/odbc-data-source-administrator?view=sql-server-2017) ，建立與 SQL Server 執行個體的測試連線。 如果資料庫已正確設定且輸入的使用者名稱和密碼皆無誤時，您應可看到剛建立的資料庫，並可將其選取為預設資料庫。
  
    連接失敗的常見原因包括伺服器未啟用遠端連線, 而且未啟用具名管道通訊協定。 您可以在這篇文章中找到更多疑難排解秘訣:針對[連接到 SQL Server 資料庫引擎進行疑難排解](https://docs.microsoft.com/sql/database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine)。
  
- **為什麼我的資料表名稱前會加上資料讀取元？**
  
    當您將此使用者的預設架構指定為**db_datareader**時, 此使用者建立的所有資料表和其他新物件都會在前面加上*架構*名稱。 結構描述就像是一個資料夾，您可以新增到資料庫以便組織物件。 結構描述也可定義資料庫內的使用者權限。
  
    當架構與一個特定的使用者名稱建立關聯時, 使用者就是_架構擁有_者。 在建立物件時，除非您特別要求要以另一個結構描述來建立，否則一律會以您自己的結構描述來建立物件。
  
    例如, 如果您建立名為**TestData**的資料表, 而您的預設架構是**db_datareader**, 則會使用名稱`<database_name>.db_datareader.TestData`來建立資料表。
  
    因此，資料庫可以包含多個具有相同名稱的資料表，只要資料表屬於不同的結構描述即可。
   
    如果您要尋找資料表, 但未指定架構, 則資料庫伺服器會尋找您所擁有的架構。 因此，如果資料表含有與您的登入相關聯的結構描述，存取這類資料表時就不需要指定結構描述名稱。
  
- **我沒有 DDL 權限，是否仍可以執行本教學課程？**
  
    是, 但您應該要求某人預先載入資料到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料表中, 然後直接跳到下一課。 在教學課程中, 會盡可能地呼叫需要 DDL 許可權的函式。

    此外, 請要求您的系統管理員授與您許可權, 並執行任何外部腳本。 無論是遠端或使用`sp_execute_external_script`, 都需要執行 R 腳本。

## <a name="next-steps"></a>後續步驟

> [!div class="nextstepaction"]
> [使用 RxSqlServerData 建立 SQL Server 資料物件](../../advanced-analytics/tutorials/deepdive-create-sql-server-data-objects-using-rxsqlserverdata.md)