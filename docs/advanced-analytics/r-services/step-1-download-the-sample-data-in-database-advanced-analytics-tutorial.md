---
title: "步驟 1︰下載範例資料 (資料庫內進階分析教學課程) | Microsoft Docs"
ms.custom: ""
ms.date: "04/19/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
dev_langs: 
  - "R"
  - "TSQL"
ms.assetid: 32a5d5ad-c58a-4669-a90d-ef296b48fcd8
caps.latest.revision: 10
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 10
---
# 步驟 1︰下載範例資料 (資料庫內進階分析教學課程)
在此步驟中，您將下載範例資料集和 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼檔案，以用於這個逐步解說。 Github 上有共用的資料和指令碼檔案，但 PowerShell 指令碼會將資料和指令碼檔案下載到您選擇的本機目錄。  
  
## 下載資料和指令碼  
  
1.  開啟 Windows PowerShell 命令主控台。  
  
    如果需要系統管理權限來建立目的地目錄，或將檔案寫入指定的目的地，請使用 [以系統管理員​​身分執行] 選項。  
  
2.  執行下列 PowerShell 命令，將參數 *DestDir* 的值變更為任何本機目錄。  我們在此處使用的預設值是 **TempRSQL**。  
  
    ```  
    $source = ‘https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/RSQL/Download_Scripts_SQL_Walkthrough.ps1’  
    $ps1_dest = “$pwd\Download_Scripts_SQL_Walkthrough.ps1”  
    $wc = New-Object System.Net.WebClient  
    $wc.DownloadFile($source, $ps1_dest)  
    .\Download_Scripts_SQL_Walkthrough.ps1 –DestDir ‘C:\tempRSQL’  
  
    ```  
  
    如果您在 *DestDir* 中指定的資料夾不存在，PowerShell 指令碼就會加以建立。  
  
    > [!TIP]  
    > 如果您收到錯誤，可藉由使用略過引數，並訂出目前工作階段變更的範圍，以僅針對這個逐步解說，將執行 PowerShell 指令碼的原則暫時設為 **不受限制**。  
    >   
    >````  
    > Set\-ExecutionPolicy Bypass \-Scope Process  
    >````   
    > 執行此命令不會導致設定變更。  
  
    按照網際網路的連線速度，下載可能需要一些時間。  
  
3.  當所有檔案皆已下載時，PowerShell 指令碼會開啟 *DestDir* 所指定的資料夾。 在 PowerShell 命令提示字元中，執行下列命令，並檢閱已下載的檔案。  
  
    ```  
    ls  
    ```  
  
    **結果：**  
  
    ![list of files downloaded by PowerShell script](../../advanced-analytics/r-services/media/rsql-devtut-filelist.PNG "list of files downloaded by PowerShell script")  
  
## 下一個步驟  
[步驟 2︰使用 PowerShell 將資料匯入 SQL Server](../../advanced-analytics/r-services/step-2-import-data-to-sql-server-using-powershell.md)  
  
## 上一個步驟  
[適用於 SQL 開發人員的資料庫內進階分析 &#40;教學課程&#41;](../../advanced-analytics/r-services/in-database-advanced-analytics-for-sql-developers-tutorial.md)  
  
## 另請參閱  
[SQL Server R Services 教學課程](../../advanced-analytics/r-services/sql-server-r-services-tutorials.md)  
  
  
  
