---
title: "判斷 SQL Server 上已安裝的 R 封裝 |Microsoft 文件"
ms.custom: 
ms.date: 10/09/2016
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9a7f7e43-b568-406c-9434-5a2ec64ec5f5
caps.latest.revision: "11"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c570f5643880b1111889e29e6de03bbff4b10e1d
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/20/2017
---
# <a name="determine-which-r-packages-are-installed-on-sql-server"></a>判斷 SQL Server 上已安裝的 R 封裝

當您安裝 SQL Server 中的機器學習服務與 R 語言選項時，安裝程式會建立執行個體相關聯的 R 封裝程式庫。 每個執行個體都有不同的套件程式庫。 封裝的程式庫都**不**執行個體之間共用，因此可能會在不同的執行個體上安裝不同的封裝。

本文說明如何判斷哪些 R 封裝會安裝為特定執行個體。

## <a name="generate-r-package-list-using-a-stored-procedure"></a>產生使用預存程序的 R 封裝清單

下列範例使用 R 函式`installed.packages()`中[!INCLUDE[tsql](..\..\includes\tsql-md.md)]預存程序取得已安裝目前的執行個體 R_SERVICES 文件庫中的封裝矩陣。 為了避免剖析 DESCRIPTION 檔案中的欄位，只會傳回名稱。

```SQL
EXECUTE sp_execute_external_script
@language=N'R'  
,@script = N'str(OutputDataSet);  
packagematrix <- installed.packages();  
NameOnly <- packagematrix[,1];  
OutputDataSet <- as.data.frame(NameOnly);'  
,@input_data_1 = N'SELECT 1 as col'  
WITH RESULT SETS ((PackageName nvarchar(250) ))  
```

如需詳細的選擇性資訊和 R 封裝 DESCRIPTION 檔案的預設欄位，請參閱[https://cran.r-project.org](https://cran.r-project.org/doc/manuals/R-exts.html#The-DESCRIPTION-file)。

## <a name="verify-whether-a-package-is-installed-with-an-instance"></a>確認封裝是否已安裝的執行個體

如果您已安裝封裝，並想要確定它是適用於特定的 SQL Server 執行個體，您可以執行下列預存程序呼叫來載入封裝，並傳回只有訊息。

```SQL
EXEC sp_execute_external_script  @language =N'R',
@script=N'library("RevoScaleR")'
GO
```

這個範例會尋找並載入 RevoScaleR 程式庫。

+ 如果找到封裝，傳回的訊息應該像是 「 命令成功完成。 」

+ 如果不能位於或載入封裝，您會收到如下錯誤: 「 發生外部指令碼錯誤： library("RevoScaleR") 時發生錯誤： 沒有呼叫 RevoScaleR 封裝 」

## <a name="get-a-list-of-installed-packages-using-r"></a>取得一份使用 R 的安裝封裝

有多種方式可以使用 R 工具和 R 函數取得已安裝或已載入封裝的清單。 許多 R 開發工具都提供物件瀏覽器或已在目前 R 工作區中安裝或載入的封裝清單。

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
## <a name="see-also"></a>另請參閱

[SQL Server 上安裝其他的 R 封裝](install-additional-r-packages-on-sql-server.md)
