---
title: 建立啟用 FILESTREAM 的資料庫 | Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], FILESTREAM-enabled databases
ms.assetid: 0fc16356-76f7-44b8-a58b-f0b7c43694ec
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 65de151b2ea2bb59330bae0fa94c9e15d67e4a47
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58533540"
---
# <a name="create-a-filestream-enabled-database"></a>建立啟用 FILESTREAM 的資料庫
  此主題說明如何建立支援 FILESTREAM 的資料庫。 因為 FILESTREAM 使用特殊類型的檔案群組，所以當您在建立資料庫時，至少必須針對一個檔案群組指定 CONTAINS FILESTREAM 子句。  
  
 FILESTREAM 檔案群組可以包含多個檔案。 如需示範如何建立包含多個檔案之 FILESTREAM 檔案群組的程式碼範例，請參閱 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)。  
  
### <a name="to-create-a-filestream-enabled-database"></a>建立啟用 FILESTREAM 的資料庫  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，按一下 **[新增查詢]** 顯示 [查詢編輯器]。  
  
2.  複製[!INCLUDE[tsql](../../includes/tsql-md.md)]程式碼會建立稱為 Archive 的啟用 FILESTREAM 的資料庫。  
  
    > [!NOTE]  
    >  在這個指令碼中，目錄 C:\Data 必須存在。  
  
3.  若要建立資料庫，請按一下 **[執行]**。  
  
## <a name="example"></a>範例  
 下列程式碼範例會建立名為 `Archive`的資料庫。 此資料庫包含三個檔案群組： `PRIMARY`、 `Arch1`和 `FileStreamGroup1`。 `PRIMARY` 和 `Arch1` 是一般的檔案群組，不能包含 FILESTREAM 資料。 `FileStreamGroup1` 則為 `FILESTREAM` 檔案群組。  
  
```sql  
CREATE DATABASE Archive   
ON  
PRIMARY ( NAME = Arch1,  
    FILENAME = 'c:\data\archdat1.mdf'),  
FILEGROUP FileStreamGroup1 CONTAINS FILESTREAM( NAME = Arch3,  
    FILENAME = 'c:\data\filestream1')  
LOG ON  ( NAME = Archlog1,  
    FILENAME = 'c:\data\archlog1.ldf')  
GO  
```  
  
 如為 `FILESTREAM` 檔案群組，則 `FILENAME` 就是指路徑。 到最後一個資料夾為止的路徑必須存在，而最後一個資料夾則不得存在。 在這個範例中， `c:\data` 必須存在。 不過，當您執行 `filestream1` 陳述式時，不能存在 `CREATE DATABASE` 子資料夾。 如需此語法的詳細資訊，請參閱 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)。  
  
 在您執行上述範例之後，filestream.hdr 檔案和 $FSLOG 資料夾就會出現在 c:\Data\filestream1 資料夾中。 filestream.hdr 檔案是 FILESTREAM 容器的標頭檔案。  
  
> [!IMPORTANT]  
>  filestream.hdr 檔案是一個重要的系統檔案， 它包含了 FILESTREAM 標頭資訊。 請勿移除或修改這個檔案。  
  
 針對現有的資料庫，您可以使用 [ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql) 陳述式來加入 FILESTREAM 檔案群組。  
  
## <a name="see-also"></a>另請參閱  
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)  
  
  
