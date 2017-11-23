---
title: "步驟 1： 下載範例資料 |Microsoft 文件"
ms.custom: 
ms.date: 10/17/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2017
dev_langs:
- Python
- TSQL
ms.assetid: 
caps.latest.revision: "2"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.openlocfilehash: b2ac1eeb53ba9f9a0dcbf86ee772db9c8b2d3553
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="step-1-download-the-sample-data"></a>步驟 1： 下載範例資料

這篇文章的教學課程中，屬於[SQL 開發人員的資料庫中的 Python 分析](sqldev-in-database-python-for-sql-developers.md)。 

Github 上共用資料，此教學課程中的指令碼。 在此步驟中，您可以使用 PowerShell 指令碼以將資料和指令碼檔案下載至您所選擇的本機目錄。

## <a name="run-the-script"></a>執行指令碼

1. 開啟 Windows PowerShell 命令主控台。

    使用選項，**系統管理員身分執行**，如果需要系統管理權限來建立目的地目錄，或將檔案寫入指定的目的地。

2. 執行下列 PowerShell 命令，將參數 *DestDir* 的值變更為任何本機目錄。  我們這裡使用預設值是`C:\temp\pysql`。

    ```ps
    $source = 'https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/PythonSQL/Download_Scripts_SQL_Walkthrough.ps1'
    $ps1_dest = "$pwd\Download_Scripts_SQL_Walkthrough.ps1"
    $wc = New-Object System.Net.WebClient
    $wc.DownloadFile($source, $ps1_dest)
    .\Download_Scripts_SQL_Walkthrough.ps1 –DestDir 'C:\temp\pysql'
    ```
    
    如果您在 *DestDir* 中指定的資料夾不存在，PowerShell 指令碼就會加以建立。
    
    如果您收到錯誤，請暫時設定執行 PowerShell 指令碼的原則**不受限制**這個逐步解說中，使用**略過**引數和範圍所做的變更目前工作階段。 執行此命令不會導致設定變更。
    
    ```ps
    Set-ExecutionPolicy Bypass -Scope Process
    ```

3. 根據您的網際網路連線，下載可能需要一些時間。 

## <a name="view-the-results"></a>檢視結果

當所有檔案皆已下載時，PowerShell 指令碼會開啟  *DestDir*所指定的資料夾。 

+ 在 PowerShell 命令提示字元中，執行下列命令，列出已下載的檔案。

    ```ps
    ls
    ```

![PowerShell 指令碼下載的檔案清單](media/sqldev-python-filelist.png "PowerShell 指令碼下載的檔案清單")

## <a name="next-step"></a>下一步

[步驟 2︰使用 PowerShell 將資料匯入 SQL Server](sqldev-py2-import-data-to-sql-server-using-powershell.md)

## <a name="previous-step"></a>上一個步驟

[資料庫內 Python 分析 SQL 開發人員](sqldev-in-database-python-for-sql-developers.md)

## <a name="see-also"></a>請參閱＜

[使用 Python 的機器學習服務](../python/sql-server-python-services.md)


