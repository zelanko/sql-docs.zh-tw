---
title: "大量複製資料到 SQL Server on Linux |Microsoft 文件"
description: 
author: sanagama
ms.author: sanagama
manager: jhubbard
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.assetid: 7b93d0d7-7946-4b78-b33a-57d6307cdfa9
ms.workload: On Demand
ms.openlocfilehash: 5796872eb1f2a0a7cdcdcd895081df6169669240
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="bulk-copy-data-with-bcp-to-sql-server-on-linux"></a>SQL Server on Linux 的 bcp 大量複製資料

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

本主題示範如何使用[bcp](../tools/bcp-utility.md) Linux 上的 SQL Server 2017 的執行個體和使用者指定格式資料檔之間大量複製資料的命令列公用程式。

您可以使用`bcp`大量的資料列匯入 SQL Server 資料表，或將資料從 SQL Server 資料表匯出至資料檔案。 Queryout 選項搭配使用時，除非`bcp`不需要知道的 Transact SQL。 `bcp`命令列公用程式的運作方式與在內部部署執行 Microsoft SQL Server，或在雲端中，有關 Linux、 Windows 或 Docker 和 Azure SQL Database 和 Azure SQL 資料倉儲。

本主題將示範如何以：
- 資料匯入至資料表，使用`bcp in`命令
- 將資料從資料表 uisng 匯出`bcp out`命令

## <a name="install-the-sql-server-command-line-tools"></a>安裝 SQL Server 命令列工具

`bcp`是 SQL Server 命令列工具，不會與 SQL Server on Linux 自動安裝的一部分。 如果您在 Linux 電腦上並沒有安裝 SQL Server 命令列工具，您必須安裝它們。 如需有關如何安裝這些工具的詳細資訊，請從下列清單中選取您的 Linux 散發套件：

- [Red Hat Enterprise Linux (RHEL)](sql-server-linux-setup-tools.md#RHEL)
- [Ubuntu](sql-server-linux-setup-tools.md#ubuntu)
- [SUSE Linux Enterprise Server (SLES)](sql-server-linux-setup-tools.md#SLES)

## <a name="import-data-with-bcp"></a>以 bcp 匯入資料

在此教學課程中，您將建立範例資料庫和資料表上的本機 SQL Server 執行個體 (**localhost**)，然後使用`bcp`載入從磁碟上的文字檔案的範例資料表。

### <a name="create-a-sample-database-and-table"></a>建立範例資料庫和資料表

現在就開始將使用在本教學課程的其餘部分的簡單資料表建立範例資料庫。

1. 在 Linux 方塊中，開啟 [命令終端機]。

2. 複製並貼到終端機視窗下方的命令。 這些命令會使用**sqlcmd**命令列公用程式，以建立範例資料庫 (**BcpSampleDB**) 和資料表 (**TestEmployees**) 上的本機 SQL Server 執行個體 (**localhost**)。 請記得要取代`username`和`<your_password>`視之前執行命令。

建立資料庫**BcpSampleDB**:
```bash 
sqlcmd -S localhost -U sa -P <your_password> -Q "CREATE DATABASE BcpSampleDB;"
```
建立資料表**TestEmployees**資料庫中**BcpSampleDB**:
```bash 
sqlcmd -S localhost -U sa -P <your_password> -d BcpSampleDB -Q "CREATE TABLE TestEmployees (Id INT IDENTITY(1,1) NOT NULL PRIMARY KEY, Name NVARCHAR(50), Location NVARCHAR(50));"
```
### <a name="create-the-source-data-file"></a>建立來源資料檔
複製並貼上以下的命令，在終端機視窗。 我們將使用內建`cat`命令以建立具有 3 個記錄的範例文字資料檔案將檔案儲存為主目錄中**~/test_data.txt**。 以逗號分隔記錄中的欄位。

```bash
cat > ~/test_data.txt << EOF
1,Jared,Australia
2,Nikita,India
3,Tom,Germany
EOF
```

您可以確認資料檔案已正確建立在終端機視窗執行下列命令：
```bash 
cat ~/test_data.txt
```

這應該在終端機視窗會顯示下列：
```bash
1,Jared,Australia
2,Nikita,India
3,Tom,Germany
```

### <a name="import-data-from-the-source-data-file"></a>從來源資料檔匯入資料
複製並貼到終端機視窗下方的命令。 此命令會使用`bcp`連接到本機 SQL Server 執行個體 (**localhost**) 和從資料檔匯入資料 (**~/test_data.txt**) 到資料表 (**TestEmployees**) 資料庫中 (**BcpSampleDB**)。 請記得要取代的使用者名稱和`<your_password>`視之前執行命令。

```bash 
bcp TestEmployees in ~/test_data.txt -S localhost -U sa -P <your_password> -d BcpSampleDB -c -t  ','
```

以下是我們搭配使用的命令列參數的簡短概觀`bcp`在此範例中：
- `-S`： 指定要連接的 SQL Server 執行個體
- `-U`： 指定的登入識別碼用來連接到 SQL Server
- `-P`： 指定的密碼登入識別碼。
- `-d`： 指定要連接到資料庫
- `-c`： 使用字元資料類型執行作業
- `-t`： 指定欄位結束字元。 我們使用`comma`作為欄位結束字元，我們的資料檔案中的資料錄

> [!NOTE]
> 我們在此範例中未指定自訂的資料列結束字元。 文字資料檔案中的資料列已正確地終止與`newline`當我們使用`cat`稍早建立的資料檔案的命令。

您可以確認資料已成功匯入您的終端機視窗中執行以下命令。 請記得要取代`username`和`<your_password>`在必要時，才能執行此命令。
```bash 
sqlcmd -S localhost -d BcpSampleDB -U sa -P <your_password> -I -Q "SELECT * FROM TestEmployees;"
```

這應會顯示下列結果：
```bash
Id          Name                Location
----------- ------------------- -------------------
          1 Jared               Australia
          2 Nikita              India
          3 Tom                 Germany

(3 rows affected)
```

## <a name="export-data-with-bcp"></a>以 bcp 匯出資料

在此教學課程中，您將使用`bcp`從我們稍早建立的新資料檔的範例資料表匯出資料。

複製並貼到終端機視窗下方的命令。 這些命令會使用`bcp`命令列公用程式將資料從資料表匯出**TestEmployees**在資料庫中**BcpSampleDB**到新的資料檔案，稱為**~/test_export.txt**。  請記得要取代的使用者名稱和`<your_password>`在必要時，才能執行此命令。

```bash 
bcp TestEmployees out ~/test_export.txt -S localhost -U sa -P <your_password> -d BcpSampleDB -c -t ','
```

您可以確認資料已正確匯出，您的終端機視窗中執行以下命令：
```bash 
cat ~/test_export.txt
```

這應該在終端機視窗會顯示下列：
```
1,Jared,Australia
2,Nikita,India
3,Tom,Germany
```

## <a name="see-also"></a>另請參閱
- [bcp 公用程式](../tools/bcp-utility.md)
- [使用 bcp 時的相容性的資料格式](../relational-databases/import-export/specify-data-formats-for-compatibility-when-using-bcp-sql-server.md)
- [使用 BULK INSERT 匯入大量資料](../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)
- [BULK INSERT (TRANSACT-SQL)](../t-sql/statements/bulk-insert-transact-sql.md)
