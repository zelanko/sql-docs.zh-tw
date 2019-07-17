---
title: 在 Linux 上 SQL server 的大量複製資料
description: ''
author: VanMSFT
ms.author: vanto
ms.date: 01/30/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 7b93d0d7-7946-4b78-b33a-57d6307cdfa9
ms.openlocfilehash: b611ef63532dd855648354bb85fc96f7cb52bd60
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68127315"
---
# <a name="bulk-copy-data-with-bcp-to-sql-server-on-linux"></a>使用 Linux 上的 SQL Server 的 bcp 大量複製資料

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

這篇文章示範如何使用[bcp](../tools/bcp-utility.md)命令列公用程式在 Linux 上的 SQL Server 的執行個體以使用者指定格式資料檔之間大量複製資料。

您可以使用`bcp`大量的資料列匯入至 SQL Server 資料表，或將資料從 SQL Server 資料表匯出至資料檔案。 除非與 queryout 選項搭配使用時`bcp`不需要知道 Transact SQL。 `bcp`命令列公用程式的運作方式與內部部署上執行的 Microsoft SQL Server，或在雲端、 Linux、 Windows 或 Docker 和 Azure SQL Database 和 Azure SQL 資料倉儲中。

本文示範如何：
- 資料匯入至資料表，使用`bcp in`命令
- 將資料從資料表使用匯出`bcp out`命令

## <a name="install-the-sql-server-command-line-tools"></a>安裝 SQL Server 命令列工具

`bcp` 是 SQL Server 命令列工具，不會使用 Linux 上的 SQL Server 自動安裝的一部分。 如果您在 Linux 機器上並沒有安裝 SQL Server 命令列工具，您必須安裝它們。 如需有關如何安裝工具的詳細資訊，請從下列清單中選取您的 Linux 散發套件：

- [Red Hat Enterprise Linux (RHEL)](sql-server-linux-setup-tools.md#RHEL)
- [Ubuntu](sql-server-linux-setup-tools.md#ubuntu)
- [SUSE Linux Enterprise Server (SLES)](sql-server-linux-setup-tools.md#SLES)

## <a name="import-data-with-bcp"></a>使用 bcp 匯入資料

在本教學課程中，您的範例資料庫和資料表上建立本機的 SQL Server 執行個體 (**localhost**)，然後使用`bcp`載入到磁碟上的文字檔案的範例資料表。

### <a name="create-a-sample-database-and-table"></a>建立範例資料庫和資料表

讓我們開始建立範例資料庫使用簡單的資料表，可在本教學課程的其餘部分。

1. 在您的 Linux 中，開啟 命令終端機。

2. 複製並貼到終端機視窗中的下列命令。 這些命令會使用**sqlcmd**若要建立範例資料庫的命令列公用程式 (**BcpSampleDB**) 和資料表 (**TestEmployees**) 本機的 SQL Server 執行個體 (**localhost**)。 請記得取代`username`和`<your_password>`視之前執行命令。

建立資料庫**BcpSampleDB**:
```bash 
sqlcmd -S localhost -U sa -P <your_password> -Q "CREATE DATABASE BcpSampleDB;"
```
建立資料表**TestEmployees**資料庫中**BcpSampleDB**:
```bash 
sqlcmd -S localhost -U sa -P <your_password> -d BcpSampleDB -Q "CREATE TABLE TestEmployees (Id INT IDENTITY(1,1) NOT NULL PRIMARY KEY, Name NVARCHAR(50), Location NVARCHAR(50));"
```
### <a name="create-the-source-data-file"></a>建立來源資料檔
複製並貼入您的終端機視窗中的下列命令。 我們會使用內建`cat`命令來建立具有三個記錄的範例文字資料檔案儲存為主目錄中的檔案 **~/test_data.txt**。 記錄中的欄位是以逗號分隔。

```bash
cat > ~/test_data.txt << EOF
1,Jared,Australia
2,Nikita,India
3,Tom,Germany
EOF
```

您可以確認資料檔案已正確建立，在您的終端機視窗中執行下列命令：
```bash 
cat ~/test_data.txt
```

這應該在您的終端機視窗會顯示下列：
```bash
1,Jared,Australia
2,Nikita,India
3,Tom,Germany
```

### <a name="import-data-from-the-source-data-file"></a>從來源資料檔匯入資料
複製並貼到終端機視窗中的下列命令。 此命令會使用`bcp`連接到本機的 SQL Server 執行個體 (**localhost**) 和從資料檔匯入資料 ( **~/test_data.txt**) 插入資料表 (**TestEmployees**) 在資料庫中 (**BcpSampleDB**)。 請記得取代使用者名稱和`<your_password>`視之前執行命令。

```bash 
bcp TestEmployees in ~/test_data.txt -S localhost -U sa -P <your_password> -d BcpSampleDB -c -t  ','
```

以下是我們搭配使用的命令列參數的簡短概觀`bcp`在此範例中：
- `-S`： 指定要連接的 SQL Server 執行個體
- `-U`： 指定的識別碼，用以連接到 SQL Server 的登入
- `-P`： 指定的密碼登入識別碼
- `-d`： 指定要連接到資料庫
- `-c`： 使用字元資料類型執行作業
- `-t`： 指定欄位結束字元。 我們會使用`comma`作為我們的資料檔案中的資料錄的欄位結束字元

> [!NOTE]
> 我們不會在此範例中，指定自訂的資料列結束字元。 在文字資料檔案中的資料列已正確地終止與`newline`當我們使用`cat`稍早建立的資料檔案的命令。

您可以確認資料已成功匯入終端機視窗中執行下列命令。 請記得取代`username`和`<your_password>`必要時再執行命令。
```bash 
sqlcmd -S localhost -d BcpSampleDB -U sa -P <your_password> -I -Q "SELECT * FROM TestEmployees;"
```

這應該會顯示下列結果：
```bash
Id          Name                Location
----------- ------------------- -------------------
          1 Jared               Australia
          2 Nikita              India
          3 Tom                 Germany

(3 rows affected)
```

## <a name="export-data-with-bcp"></a>使用 bcp 匯出資料

在本教學課程中，您可以使用`bcp`從我們稍早建立新的資料檔案的範例資料表匯出資料。

複製並貼到終端機視窗中的下列命令。 這些命令會使用`bcp`將資料從資料表匯出的命令列公用程式**TestEmployees**資料庫中**BcpSampleDB**到新的資料檔案，稱為 **~/test_export.txt**.  請記得取代使用者名稱和`<your_password>`必要時再執行命令。

```bash 
bcp TestEmployees out ~/test_export.txt -S localhost -U sa -P <your_password> -d BcpSampleDB -c -t ','
```

您可以確認資料已正確匯出，藉由在終端機視窗中執行下列命令：
```bash 
cat ~/test_export.txt
```

這應該在您的終端機視窗會顯示下列：
```
1,Jared,Australia
2,Nikita,India
3,Tom,Germany
```

## <a name="see-also"></a>另請參閱
- [bcp 公用程式](../tools/bcp-utility.md)
- [使用 bcp 時的相容性的資料格式](../relational-databases/import-export/specify-data-formats-for-compatibility-when-using-bcp-sql-server.md)
- [使用 BULK INSERT 匯入大量資料](../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)
- [BULK INSERT (Transact-SQL)](../t-sql/statements/bulk-insert-transact-sql.md)
