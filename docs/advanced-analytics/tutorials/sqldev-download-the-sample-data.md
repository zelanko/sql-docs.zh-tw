---
title: "第 1 課： 下載範例資料 |Microsoft 文件"
ms.custom: 
ms.date: 07/26/2016
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to:
- SQL Server 2016
dev_langs:
- R
- TSQL
ms.assetid: 32a5d5ad-c58a-4669-a90d-ef296b48fcd8
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: aa58a4f64717b7ccf2be335a58ae4838b283dd44
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2018
---
# <a name="lesson-1-download-the-sample-data"></a>第 1 課： 下載範例資料
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

這篇文章是有關如何在 SQL Server 中使用 R 的 SQL 開發人員的教學課程的一部分。

在此步驟中，您將下載的範例資料集和[!INCLUDE[tsql](../../includes/tsql-md.md)]指令碼會用於本教學課程中的檔案。 GitHub 上共用資料和指令碼檔案，但 PowerShell 指令碼會下載至您所選擇的本機目錄的資料和指令碼檔案。

## <a name="download-the-data-and-scripts"></a>下載的資料和指令碼

1.  開啟 Windows PowerShell 命令主控台。
  
    如果需要系統管理權限來建立目的地目錄，或將檔案寫入指定的目的地，請使用 [以系統管理員​​身分執行] 選項。
  
2.  執行下列 PowerShell 命令，將參數 *DestDir* 的值變更為任何本機目錄。  我們在此處使用的預設值是 **TempRSQL**。
  
    ```ps
    $source = ‘https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/RSQL/Download_Scripts_SQL_Walkthrough.ps1’  
    $ps1_dest = “$pwd\Download_Scripts_SQL_Walkthrough.ps1”
    $wc = New-Object System.Net.WebClient
    $wc.DownloadFile($source, $ps1_dest)
    .\Download_Scripts_SQL_Walkthrough.ps1 –DestDir ‘C:\tempRSQL’
    ```
  
    如果您在 *DestDir* 中指定的資料夾不存在，PowerShell 指令碼就會加以建立。
  
    > [!TIP]
    > 如果您收到錯誤，可藉由使用略過引數，並訂出目前工作階段變更的範圍，以僅針對這個逐步解說，將執行 PowerShell 指令碼的原則暫時設為 **不受限制** 。
    >   
    >````
    > Set\-ExecutionPolicy Bypass \-Scope Process
    >````
    > 執行此命令不會導致設定變更。
  
    按照網際網路的連線速度，下載可能需要一些時間。
  
3.  當所有檔案皆已下載時，PowerShell 指令碼會開啟  *DestDir*所指定的資料夾。 在 PowerShell 命令提示字元中，執行下列命令，並檢閱已下載的檔案。
  
    ```
    ls
    ```
  
    **結果：**
  
    ![PowerShell 指令碼下載的檔案清單](media/rsql-devtut-filelist.png "PowerShell 指令碼下載的檔案清單")
  
## <a name="next-lesson"></a>下一課

[第 2 課： 將資料匯入 SQL Server 使用 PowerShell](../r/sqldev-import-data-to-sql-server-using-powershell.md)

## <a name="previous-lesson"></a>上一課

[資料庫中的 SQL 開發人員的 R 分析](../tutorials/sqldev-in-database-r-for-sql-developers.md)
