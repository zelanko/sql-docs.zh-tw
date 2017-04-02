---
title: "決定要安裝在 SQL Server 上的封裝 | Microsoft Docs"
ms.custom: ""
ms.date: "08/31/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 9a7f7e43-b568-406c-9434-5a2ec64ec5f5
caps.latest.revision: 11
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 10
---
# 決定要安裝在 SQL Server 上的封裝
  本主題說明如何判斷哪些 R 套件安裝在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。  
  
根據預設，安裝的 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 會建立每個執行個體相關聯的 R 封裝程式庫。 因此，知道哪些封裝安裝在電腦上，您必須安裝 R Services 每個個別執行個體上執行此查詢。 請注意，封裝程式庫是 **不** 執行個體之間共用，因此可能會在不同的執行個體上安裝不同的封裝。

如需如何判斷執行個體的預設程式庫位置資訊，請參閱 [安裝和管理的 R 封裝](../../advanced-analytics/r-services/installing-and-managing-r-packages.md)。   
   
 
## 取得一份已安裝的封裝使用 R  
 有多種方式可以取得已安裝或載入封裝使用 R 工具和 R 函數的清單。  
  
+   許多 R 開發工具都提供物件瀏覽器或已在目前 R 工作區中安裝或載入的封裝清單。  

+ 我們建議您從 RevoScaleR 封裝特別提供管理套件中的下列函式計算內容︰
  - [rxFindPackage](https://msdn.microsoft.com/microsoft-r/scaler/rxfindpackage)
  - [rxInstalledPackages](https://msdn.microsoft.com/microsoft-r/scaler/rxInstalledPackages)   
  
+   您可以使用的 R 函式，例如 `installed.packages()`, ，這是包含在已安裝 `utils` 封裝。 函式會掃描指定的媒體櫃中找不到，並傳回封裝的名稱、 程式庫路徑和版本號碼的矩陣的每個套件的描述檔案。  
 
### 範例  
下列範例會使用函式 `rxInstalledPackages` 取得封裝所提供的 SQL Server 計算內容中可用的清單。

~~~~
sqlServerCompute <- RxInSqlServer(connectionString = 
"Driver=SQL Server;Server=myServer;Database=TestDB;Uid=myID;Pwd=myPwd;")
     sqlPackages <- rxInstalledPackages(computeContext = sqlServerCompute)
     sqlPackages
~~~~

 下列範例會使用基底的 R 函數 `installed.packages()` 中 [!INCLUDE[tsql](../../includes/tsql-md.md)] 預存程序，以取得目前執行個體 R_SERVICES 文件庫中已安裝的封裝的矩陣。 為了避免剖析 DESCRIPTION 檔案中的欄位，只會傳回名稱。  
  
```  
EXECUTE sp_execute_external_script  
@language=N'R'  
,@script = N'str(OutputDataSet);  
packagematrix <- installed.packages();  
NameOnly <- packagematrix[,1];  
OutputDataSet <- as.data.frame(NameOnly);'  
,@input_data_1 = N'SELECT 1 as col'  
WITH RESULT SETS ((PackageName nvarchar(250) ))  
```  
  
 如需預設和選擇性欄位中的 R 封裝描述檔案的詳細資訊，請參閱 [https://cran.r-project.org/doc/manuals/R-exts.html#The-DESCRIPTION-file](https://cran.r-project.org/doc/manuals/R-exts.html)。  
  
## 另請參閱  
 [在 SQL Server 上安裝其他的 R 封裝](../../advanced-analytics/r-services/install-additional-r-packages-on-sql-server.md)  
  
  