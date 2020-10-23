---
title: 將資料大量複製到 Linux 上的 SQL Server
description: 本文描述 bcp 公用程式。 使用 bcp 將大量資料列匯入 SQL Server 資料表中，或將 SQL Server 資料表的資料匯出至資料檔案中。
author: VanMSFT
ms.author: vanto
ms.date: 01/30/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 7b93d0d7-7946-4b78-b33a-57d6307cdfa9
ms.openlocfilehash: 1d4c924652ec21ab4ed8e7c79d01d7f36835715b
ms.sourcegitcommit: a5398f107599102af7c8cda815d8e5e9a367ce7e
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/13/2020
ms.locfileid: "92006559"
---
# <a name="bulk-copy-data-with-bcp-to-sql-server-on-linux"></a>使用 bcp 將資料大量複製到 Linux 上的 SQL Server

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

此文章說明如何使用 [bcp](../tools/bcp-utility.md) 命令列公用程式，在 Linux 上的 SQL Server 的執行個體與使用者指定格式的資料檔案之間大量複製資料。

您可以使用 `bcp` 將大量資料列匯入 SQL Server 資料表中，或將 SQL Server 資料表的資料匯出至資料檔中。 除了搭配 queryout 選項使用之外，`bcp` 不需要任何 Transact-SQL 的知識。 `bcp` 命令列公用程式可搭配在內部部署或雲端中、於 Linux、Windows 或 Docker 上執行的 Microsoft SQL Server，以及 Azure SQL Database 和 Azure Synapse Analytics 使用。

本文示範如何：
- 使用 `bcp in` 命令將資料匯入資料表
- 使用 `bcp out` 命令從資料表匯出資料

## <a name="install-the-sql-server-command-line-tools"></a>安裝 SQL Server 命令列工具

`bcp` 是 SQL Server 命令列工具的一部分，這些工具不會隨 Linux 上的 SQL Server 自動安裝。 如果您尚未在 Linux 機器上安裝 SQL Server 命令列工具，您必須安裝它們。 如需有關如何安裝工具的詳細資訊，請從下列清單中選取您的 Linux 散發套件：

- [Red Hat Enterprise Linux (RHEL)](sql-server-linux-setup-tools.md#RHEL)
- [Ubuntu](sql-server-linux-setup-tools.md#ubuntu)
- [SUSE Linux Enterprise Server (SLES)](sql-server-linux-setup-tools.md#SLES)

## <a name="import-data-with-bcp"></a>使用 bcp 匯入資料

在本教學課程中，您會在本機 SQL Server 執行個體 (**localhost**) 上建立範例資料庫和資料表，然後使用 `bcp` 從磁碟上的文字檔載入至範例資料表。

### <a name="create-a-sample-database-and-table"></a>建立範例資料庫與資料表

讓我們從使用在本教學課程的其餘部分所使用的簡單資料表來建立範例資料庫開始。

1. 在您的 Linux 方塊上，開啟命令終端機。

2. 複製下列命令並貼到終端機視窗中。 這些命令會使用 **sqlcmd** 命令列公用程式，在本機 SQL Server 執行個體 (**localhost**) 上建立範例資料庫 (**BcpSampleDB**) 和資料表 (**TestEmployees**)。 請記得在執行命令之前，視需要取代 `username` 和 `<your_password>`。

建立資料庫 **BcpSampleDB**：
```bash 
sqlcmd -S localhost -U sa -P <your_password> -Q "CREATE DATABASE BcpSampleDB;"
```
在資料庫 **BcpSampleDB** 中建立資料表 **TestEmployees**：
```bash 
sqlcmd -S localhost -U sa -P <your_password> -d BcpSampleDB -Q "CREATE TABLE TestEmployees (Id INT IDENTITY(1,1) NOT NULL PRIMARY KEY, Name NVARCHAR(50), Location NVARCHAR(50));"
```
### <a name="create-the-source-data-file"></a>建立來源資料檔案
複製下列命令並貼到您的終端機視窗中。 我們使用內建的 `cat` 命令來建立包含三筆記錄的範例文字資料檔案，並將檔案儲存在您的主目錄中 ( **~/test_data.txt**)。 記錄中的欄位會以逗號分隔。

```bash
cat > ~/test_data.txt << EOF
1,Jared,Australia
2,Nikita,India
3,Tom,Germany
EOF
```

您可以在終端機視窗中執行下列命令，以確認資料檔案已正確建立：
```bash 
cat ~/test_data.txt
```

這應該會在您的終端機視窗中顯示下列內容：
```bash
1,Jared,Australia
2,Nikita,India
3,Tom,Germany
```

### <a name="import-data-from-the-source-data-file"></a>從來源資料檔案匯入資料
複製下列命令並貼到終端機視窗中。 此命令會使用 `bcp` 來連線至本機 SQL Server 執行個體 (**localhost**)，並將資料從資料檔 ( **~/test_data.txt**) 匯入到資料庫 (**BcpSampleDB**) 中的資料表 (**TestEmployees**)。 在執行命令之前，請記住視需要取代使用者名稱和 `<your_password>`。

```bash 
bcp TestEmployees in ~/test_data.txt -S localhost -U sa -P <your_password> -d BcpSampleDB -c -t  ','
```

以下簡要介紹我們在此範例中搭配 `bcp` 使用的命令列參數：
- `-S`：指定要連線的 SQL Server 執行個體
- `-U`：指定用來連接至 SQL Server 的登入識別碼
- `-P`：指定登入識別碼的密碼
- `-d`：指定要連線的資料庫
- `-c`：利用字元資料類型來執行作業
- `-t`：指定欄位結束字元。 我們會使用 `comma` 作為資料檔案中記錄的欄位結束字元

> [!NOTE]
> 在此範例中，我們不會指定自訂的資料列結束字元。 當我們稍早使用 `cat` 命令來建立資料檔案時，文字資料檔案中的資料列已正確地以 `newline` 終止。

您可以在終端機視窗中執行下列命令，以確認資料已成功匯入。 請記得在執行命令之前，視需要取代 `username` 和 `<your_password>`。
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

## <a name="export-data-with-bcp"></a>使用 bcp 匯入資料

在本教學課程中，您會使用 `bcp` 從我們稍早建立的範例資料表中，將資料匯出到新的資料檔案。

複製下列命令並貼到終端機視窗中。 這些命令會使用 `bcp` 命令列公用程式，將資料從資料庫 **BcpSampleDB** 中的資料表 **TestEmployees**，匯出到名為 **~/test_export.txt** 的新資料檔案。  在執行命令之前，請記住視需要取代使用者名稱和 `<your_password>`。

```bash 
bcp TestEmployees out ~/test_export.txt -S localhost -U sa -P <your_password> -d BcpSampleDB -c -t ','
```

您可以在終端機視窗中執行下列命令，以確認資料檔案已正確匯出：
```bash 
cat ~/test_export.txt
```

這應該會在您的終端機視窗中顯示下列內容：
```
1,Jared,Australia
2,Nikita,India
3,Tom,Germany
```

## <a name="see-also"></a>另請參閱
- [bcp 公用程式](../tools/bcp-utility.md)
- [使用 bcp 時的相容性資料格式](../relational-databases/import-export/specify-data-formats-for-compatibility-when-using-bcp-sql-server.md)
- [使用 BULK INSERT 匯入大量資料](../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)
- [BULK INSERT (Transact-SQL)](../t-sql/statements/bulk-insert-transact-sql.md)
