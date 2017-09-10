---
title: "決定要安裝在 SQL Server 上的封裝 | Microsoft Docs"
ms.custom: 
ms.date: 08/31/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9a7f7e43-b568-406c-9434-5a2ec64ec5f5
caps.latest.revision: 11
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 90e7146bde123ca8ac8a8e6ff3e11d212fd4a35a
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="determine-which-packages-are-installed-on-sql-server"></a>決定要安裝在 SQL Server 上的封裝
  本主題說明如何判斷有哪些 R 套件安裝在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上。  
  
根據預設，[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 的安裝會建立與每個執行個體相關聯的 R 封裝程式庫。 因此，若要知道有哪些封裝安裝在電腦上，您必須在安裝 R 服務的每個個別執行個體上執行此查詢。 請注意，封裝程式庫「不會」在執行個體之間共用，因此可能會在不同的執行個體上安裝不同的封裝。

如需如何判斷執行個體之預設程式庫位置的資訊，請參閱[安裝和管理的 R 封裝](../../advanced-analytics/r-services/installing-and-managing-r-packages.md)。   
   
 
## <a name="get-a-list-of-installed-packages-using-r"></a>使用 R 取得已安裝封裝的清單  
 有多種方式可以使用 R 工具和 R 函數取得已安裝或已載入封裝的清單。  
  
+   許多 R 開發工具都提供物件瀏覽器或已在目前 R 工作區中安裝或載入的封裝清單。  

+ 我們建議使用以下來自 RevoScaleR 封裝的函數，它們是特別針對計算內容中的封裝管理而提供︰
  - [rxFindPackage (英文)](https://msdn.microsoft.com/microsoft-r/scaler/packagehelp/rxfindpackage)
  - [rxInstalledPackages (英文)](https://msdn.microsoft.com/microsoft-r/scaler/packagehelp/rxinstalledpackages)   
  
+   您可以使用已安裝 `installed.packages()` 封裝中所含的 R 函數 (例如 `utils`)。 此函數會掃描所指定程式庫中每個封裝的 DESCRIPTION 檔案，並傳回封裝名稱、程式庫路徑和版本號碼的矩陣。  
 
### <a name="examples"></a>範例  
下列範例會使用函數 `rxInstalledPackages` 取得所提供 SQL Server 計算內容中的可用封裝清單。

~~~~
sqlServerCompute <- RxInSqlServer(connectionString = 
"Driver=SQL Server;Server=myServer;Database=TestDB;Uid=myID;Pwd=myPwd;")
     sqlPackages <- rxInstalledPackages(computeContext = sqlServerCompute)
     sqlPackages
~~~~

 下列範例會在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 預存程序中使用基底 R 函數 `installed.packages()`，以取得已在目前執行個體的 R_SERVICES 程式庫中安裝之封裝的矩陣。 為了避免剖析 DESCRIPTION 檔案中的欄位，只會傳回名稱。  
  
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
  
 如需詳細資訊，請於 [https://cran.r-project.org (英文)](https://cran.r-project.org/doc/manuals/R-exts.html#The-DESCRIPTION-file) 參閱 R 封裝 DESCRIPTION 檔案的選擇性及預設欄位描述。  
  
## <a name="see-also"></a>另請參閱  
 [在 SQL Server 上安裝其他的 R 封裝](../../advanced-analytics/r-services/install-additional-r-packages-on-sql-server.md)  
  
  

