---
title: "建立資料庫 （SQL Server 匯入和匯出精靈） |Microsoft 文件"
ms.custom: 
ms.date: 02/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.impexpwizard.createdatabase.f1
ms.assetid: 56a8a79f-086c-4bdc-8888-0045bb4b0cbf
caps.latest.revision: 54
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 3f8c2b652515f4c84121dcf14371a9e86c8f86f2
ms.contentlocale: zh-tw
ms.lasthandoff: 09/26/2017

---
# <a name="create-database-sql-server-import-and-export-wizard"></a>建立資料庫 (SQL Server 匯入和匯出精靈)
如果您在 [選擇目的地]  頁面上選取 [新增]  來建立新的 SQL Server 目的地資料庫，[ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 匯入和匯出精靈] 會顯示 [建立資料庫]  對話方塊。 在此頁面中提供新資料庫的名稱。 (選擇性) 您也可以變更新資料庫及其記錄檔的初始大小和自動成長等設定。 

**Create Database**對話方塊，在精靈中的提供僅可用於建立新的 SQL Server 資料庫的基本選項。 若要查看及對新設定的所有選項[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫，請使用[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]建立資料庫，或設定資料庫之後，精靈會建立它。 

> [!NOTE]
> 如果您想要尋找 [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE DATABASE 陳述式的相關資訊，而不是 [[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 匯入和匯出精靈] 之 [建立資料庫] 對話方塊的相關資訊，請參閱 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)。  

## <a name="screen-shot-of-the-create-database-page"></a>[建立資料庫] 頁面的螢幕擷取畫面  
下列螢幕擷取畫面顯示精靈的 [建立資料庫]  對話方塊。  

![建立資料庫 頁面上的匯入和匯出精靈](../../integration-services/import-export-data/media/create-database.png "匯入和匯出精靈建立資料庫 頁面")  

## <a name="provide-a-name-for-the-new-database"></a>提供新資料庫的名稱  
**名稱**  
 提供目的地 SQL Server 資料庫的名稱。
 
### <a name="naming-requirements"></a>命名需求
當您命名資料庫時，請確認遵循 SQL Server 命名慣例。  
  
-   資料庫名稱在 SQL Server 執行個體內必須是唯一的。  
  
-   資料庫名稱最多可有 123 個字元。 (這可讓 SQL Server 附加 5 個字元的尾碼到資料檔案和記錄檔，保持在最大值 128 個字元以內。)  
  
-   資料庫名稱必須符合 SQL Server 識別碼的規則。 以下是最重要的需求。  
  
    -   第一個字元必須是字母、底線 (_)、at 符號 (@)，或數字符號 (#)。  
  
    -   接下來的字元可以是字母、數字、符號、錢幣符號 ($)、數字符號或底線。  
  
    -   您無法使用空格或其他特殊字元。  
  
如需這些需求的詳細資訊，請參閱 [資料庫識別碼](../../relational-databases/databases/database-identifiers.md)。  

## <a name="optionally-specify-data-file-and-log-file-options"></a>選擇性指定資料檔案和記錄檔選項

> [!TIP]
> 您必須在 [名稱]  欄位中提供新資料庫的名稱，但是通常可以將檔案大小和檔案成長的其他設定保留為預設值。

### <a name="data-file-options"></a>資料檔案選項  
 **初始大小**  
 指定資料檔的初始大小 (以 MB 為單位)。  
  
 **不允許成長**  
 指出資料檔是否可以成長超過指定的初始大小。  
  
 **依百分比成長**  
 指定資料檔可以成長的百分比。  
  
 **依大小成長**  
 指定資料檔可以成長的大小 (以 MB 為單位)。  
  
### <a name="log-file-options"></a>記錄檔選項  
 **初始大小**  
 指定記錄檔的初始大小 (以 MB 為單位)。  
  
 **不允許成長**  
 指出記錄檔是否可以成長超過指定的初始大小。  
  
 **依百分比成長**  
 指定記錄檔可以成長的百分比。  
  
 **依大小成長**  
 指定記錄檔可以成長的大小 (以 MB 為單位)。  

### <a name="more-info"></a>其他資訊
如需您在此頁面看到之檔案大小選項的詳細資訊，請參閱 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)。 

## <a name="whats-next"></a>下一步  
 在您提供精靈將建立之新資料庫的名稱並按一下 [確定] 之後，[建立資料庫]  對話方塊會讓您回到 [選擇目的地]  頁面。 如需詳細資訊，請參閱 [選擇目的地](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)。  


