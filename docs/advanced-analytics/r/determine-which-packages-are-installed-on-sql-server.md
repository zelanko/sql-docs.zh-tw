---
title: "判斷 SQL Server 上已安裝的 R 封裝 |Microsoft 文件"
ms.custom: 
ms.date: 01/04/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9a7f7e43-b568-406c-9434-5a2ec64ec5f5
caps.latest.revision: "11"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: e76a42ead115c8ee4fa89599b192d722ecfbb2ee
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="determine-which-r-packages-are-installed-on-sql-server"></a>判斷 SQL Server 上已安裝的 R 封裝

當您安裝 SQL Server 中的機器學習服務與 R 語言選項時，R 封裝程式庫，將會建立專門用於執行個體。 在伺服器上的每個執行個體都有它自己的封裝程式庫。 封裝程式庫無法執行個體之間共用。

本文說明如何判斷哪些 R 封裝會安裝特定的 SQL Server 執行個體。

## <a name="generate-r-package-list-using-a-stored-procedure"></a>產生使用預存程序的 R 封裝清單

下列範例使用 R 函式`installed.packages()`中[!INCLUDE[tsql](..\..\includes\tsql-md.md)]預存程序取得已安裝目前的執行個體 R_SERVICES 文件庫中的封裝矩陣。 為了避免剖析 DESCRIPTION 檔案中的欄位，只會傳回名稱。

```SQL
EXECUTE sp_execute_external_script
@language=N'R'
,@script = N'str(OutputDataSet);
packagematrix <- installed.packages();
NameOnly <- packagematrix[,1];
OutputDataSet <- as.data.frame(NameOnly);'
, @input_data_1 = N''
WITH RESULT SETS ((PackageName nvarchar(250) ))
```

如需詳細的選擇性資訊和 R 封裝的描述欄位的預設欄位，請參閱[https://cran.r-project.org](https://cran.r-project.org/doc/manuals/R-exts.html#The-DESCRIPTION-file)。

## <a name="verify-whether-a-package-is-installed-with-an-instance"></a>確認封裝是否已安裝的執行個體

如果您已安裝封裝，並想要確定它是適用於特定的 SQL Server 執行個體，您可以執行下列預存程序呼叫來載入封裝，並傳回只有訊息。 這個範例會尋找並載入 RevoScaleR 程式庫中，如果有的話。

```sql
EXEC sp_execute_external_script  @language =N'R',
@script=N'library("RevoScaleR")'
GO
```

+ 如果找到封裝，傳回一則訊息: 「 命令成功完成。 」

+ 如果不能位於或載入封裝，您會收到含有文字錯誤: 「 有 」 呼叫 'MissingPackageName' 沒有封裝

## <a name="get-a-list-of-installed-packages-using-r"></a>取得一份使用 R 的安裝封裝

有多種方式可以使用 R 工具和 R 函數取得已安裝或已載入封裝的清單。 許多 R 開發工具都提供物件瀏覽器或已在目前 R 工作區中安裝或載入的封裝清單。 本節提供一些簡短的命令可讓您從任何 R 命令列或預存程序中\_執行\_外部\_指令碼。

+ 從本機的 R 公用程式，使用基底 R 函數，例如`installed.packages()`，隨附於`utils`封裝。 若要取得正確的執行個體的清單，您必須明確地指定程式庫路徑，或使用與執行個體文件庫相關聯的 R 工具。

+ 若要檢查特定的計算內容中的封裝，您可以使用 RevoScaleR 封裝中的下列函式。 這些函式可協助您識別封裝中指定的計算內容：

+ [rxFindPackage (英文)](https://msdn.microsoft.com/microsoft-r/scaler/packagehelp/rxfindpackage)

+ [rxInstalledPackages (英文)](https://msdn.microsoft.com/microsoft-r/scaler/packagehelp/rxinstalledpackages)

例如，執行下列 R 程式碼，以取得指定的 SQL Server 計算內容中可用的封裝清單。

```r
sqlServerCompute <- RxInSqlServer(connectionString = "Driver=SQL Server;Server=myServer;Database=TestDB;Uid=myID;Pwd=myPwd;")
sqlPackages <- rxInstalledPackages(computeContext = sqlServerCompute)
sqlPackages
```

## <a name="get-library-location-and-version"></a>取得程式庫位置和版本

下列範例會取得在本機計算內容和封裝版本的 RevoScaleR 文件庫位置。

```r
rxFindPackage(RevoScaleR, "local")
packageVersion("RevoScaleR")
```

## <a name="determine-path-of-library-used-by-sql-server"></a>判斷 SQL Server 所使用的程式庫路徑

如果您已升級的機器學習使用繫結元件，可能會變更的 R 程式庫的路徑。 當發生這種情況時，R 工具的上一個捷徑可能會參考先前的版本。 為了確保的 SQL Server 所使用的路徑及封裝版本，您可以執行的命令如下所示：

```sql
EXEC sp_execute_external_script
    @language =N'R',
    @script=N'
    sql_r_path <- rxSqlLibPaths("local")
      print(sql_r_path)
    version_info <-packageVersion("RevoScaleR")
      print(version_info)'
```

**結果**

```text
STDOUT message(s) from external script: 
[1] "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER1000/R_SERVICES/library"
[1] '9.2.1'
```
## <a name="see-also"></a>另請參閱

[SQL Server 上安裝其他的 R 封裝](install-additional-r-packages-on-sql-server.md)
