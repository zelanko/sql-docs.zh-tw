---
title: "使用 SQL Server 資料使用 R （SQL 與 R 深入探討） |Microsoft 文件"
ms.date: 12/14/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to:
- SQL Server 2016
- SQL Server 2017
dev_langs:
- R
ms.assetid: 0a3d7ba0-4113-4cde-9645-debba45cae8f
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: cf492948ad5e5e0f933deb6f3e758d0f31c5db70
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2018
---
# <a name="work-with-sql-server-data-using-r-sql-and-r-deep-dive"></a>使用 SQL Server 資料使用 R （SQL 與 R 深入探討）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文是資料科學深入探討教學課程中，有關如何使用一部分[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)與 SQL Server。

在這一課，您可以設定環境和新增您需要用於定型模型的資料並執行資料的部分快速摘要。 處理程序的一部分，您必須完成這些工作：
  
- 建立新的資料庫來儲存資料，以定型和評分兩個 R 模型。
  
- 建立帳戶 (Windows 使用者或 SQL 登入) 以供您的工作站與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 電腦之間通訊時使用。
  
- 使用 R 建立資料來源，以搭配使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料和資料庫物件。
  
- 使用 R 資料來源，將資料載入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。
  
- 使用 R 來取得變數的清單，並修改 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表的中繼資料。
  
- 建立計算內容，以遠端執行 R 程式碼。
  
- （選擇性）啟用遠端計算內容上的追蹤。
  
## <a name="create-the-database-and-user"></a>建立資料庫和使用者

這個逐步解說中，建立新的資料庫中[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]，並加入寫入和讀取資料，以及執行 R 指令碼的權限的 SQL 登入。

> [!NOTE]
> 如果您只會讀取資料，執行 R 指令碼的帳戶需要 SELECT 權限 (**db_datareader**角色) 上指定的資料庫。 不過，在本教學課程中，您必須具有 DDL 管理員權限來準備資料庫，以及建立計分結果儲存的資料表。
> 
> 此外，如果您不是資料庫擁有者，您需要有使用權限，EXECUTE ANY EXTERNAL SCRIPT，才能執行 R 指令碼。

1. 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，選取已啟用 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 的執行個體，再以滑鼠右鍵按一下 [資料庫]，然後選取 [新增資料庫]。
  
2. 輸入新資料庫的名稱。 您可以使用任意名稱；只要記得按照此逐步解說，編輯所有 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼和 R 指令碼即可。
  
    > [!TIP]
    > 若要檢視更新的資料庫名稱，請以滑鼠右鍵按一下 [資料庫]，然後選取 [重新整理]。
  
3. 將資料庫內容變更為 master 資料庫並按一下 [新增查詢]。
  
4. 在新的 [查詢] 視窗中，執行下列命令以建立使用者帳戶，並將帳戶指派給此教學課程中所用的資料庫。 請務必視需要變更資料庫名稱。
  
**Windows 使用者**
  
```SQL
 -- Create server user based on Windows account
USE master
GO
CREATE LOGIN [<DOMAIN>\<user_name>] FROM WINDOWS WITH DEFAULT_DATABASE=[DeepDive]

 --Add the new user to tutorial database
USE [DeepDive]
GO
CREATE USER [<user_name>] FOR LOGIN [<DOMAIN>\<user_name>] WITH DEFAULT_SCHEMA=[db_datareader]
```

**SQL 登入**

```SQL
-- Create new SQL login
USE master
GO
CREATE LOGIN DDUser01 WITH PASSWORD='<type password here>', CHECK_EXPIRATION=OFF, CHECK_POLICY=OFF;

-- Add the new SQL login to tutorial database
USE [DeepDive]
GO
CREATE USER [DDUser01] FOR LOGIN [DDUser01] WITH DEFAULT_SCHEMA=[db_datareader]
```

5. 若要確認已建立使用者，請選取新的資料庫，依序展開 [安全性] 和 [使用者]。

## <a name="troubleshooting"></a>疑難排解

本節列出在資料庫設定過程中可能發生的一些常見問題。

- **如何確認資料庫連線和檢查 SQL 查詢？**
  
    在使用伺服器執行 R 程式碼之前，您可能想檢查資料庫是否能與 R 開發環境連線。 [Visual Studio 中的伺服器總管](https://msdn.microsoft.com/library/x603htbk.aspx) 和 [SQL Server Management Studio](../../ssms/download-sql-server-management-studio-ssms.md) 都是免費工具，具有功能強大的資料庫連線和管理功能。
  
    如果您不想安裝其他資料庫管理工具，可以使用控制台的 [ODBC 資料來源管理員](https://msdn.microsoft.com/library/ms714024.aspx) ，建立與 SQL Server 執行個體的測試連線。 如果資料庫已正確設定且輸入的使用者名稱和密碼皆無誤時，您應可看到剛建立的資料庫，並可將其選取為預設資料庫。
  
    如果您無法連接到資料庫，請確認伺服器已啟用遠端連線，亦已啟用具名管道通訊協定。 這篇文章中所提供的其他疑難排解提示：[疑難排解連接到 SQL Server Database Engine](https://docs.microsoft.com/sql/database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine)。
  
- **為什麼我的資料表名稱前會加上資料讀取元？**
  
    當您指定做為此使用者的預設結構描述**db_datareader**，前面加上所有資料表和其他新的物件，此使用者建立的*結構描述*名稱。 結構描述就像是一個資料夾，您可以新增到資料庫以便組織物件。 結構描述也可定義資料庫內的使用者權限。
  
    一個特定的使用者名稱與相關聯的結構描述時，使用者是_結構描述擁有者_。 在建立物件時，除非您特別要求要以另一個結構描述來建立，否則一律會以您自己的結構描述來建立物件。
  
    例如，如果您建立的資料表名稱`*`TestData`, and your default schema is **db\_datareader**, the table is created with the name `.db_datareader < 資料庫名稱 >。TestData'。
  
    因此，資料庫可以包含多個具有相同名稱的資料表，只要資料表屬於不同的結構描述即可。
   
    如果您要尋找的資料表，並不指定結構描述，您所擁有的結構描述會尋找資料庫伺服器。 因此，如果資料表含有與您的登入相關聯的結構描述，存取這類資料表時就不需要指定結構描述名稱。
  
- **我沒有 DDL 權限，是否仍可以執行本教學課程？**
  
    是；不過您應該先請使用者預先載入資料至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表，並跳過呼叫建立新資料表的區段。 需要 DDL 的權限的函式會呼叫在本教學課程中可能的情況下。

    此外，請要求您的系統管理員授與您的權限，EXECUTE ANY EXTERNAL SCRIPT。 在需要執行 R 指令碼，遠端還是使用`sp_execute_external_script`。

## <a name="next-step"></a>下一步

[使用 RxSqlServerData 建立 SQL Server 資料物件](../../advanced-analytics/tutorials/deepdive-create-sql-server-data-objects-using-rxsqlserverdata.md)

## <a name="overview"></a>概觀

[資料科學深入探討︰使用 RevoScaleR 套件](../../advanced-analytics/tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)



