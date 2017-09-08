---
title: "步驟 1： 下載範例資料 |Microsoft 文件"
ms.custom: 
ms.date: 05/25/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2017
dev_langs:
- Python
- TSQL
ms.assetid: 
caps.latest.revision: 2
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 147860e9af8cce86d1a7ccbd3e53f20d240fcd49
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="step-1-download-the-sample-data"></a>步驟 1︰下載範例資料

在此步驟中，您將下載的範例資料集和指令碼。 Github 上有共用的資料和指令碼檔案，但 PowerShell 指令碼會將資料和指令碼檔案下載到您選擇的本機目錄。

## <a name="download-the-data-and-scripts"></a>下載資料和指令碼

1. 開啟 Windows PowerShell 命令主控台。

    使用選項，**系統管理員身分執行**，如果需要系統管理權限來建立目的地目錄，或將檔案寫入指定的目的地。

2. 執行下列 PowerShell 命令，將參數 *DestDir* 的值變更為任何本機目錄。  我們這裡使用預設值是**TempPythonSQL**。

    ```
    $source = 'https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/PythonSQL/Download_Scripts_SQL_Walkthrough.ps1'
    $ps1_dest = "$pwd\Download_Scripts_SQL_Walkthrough.ps1"
    $wc = New-Object System.Net.WebClient
    $wc.DownloadFile($source, $ps1_dest)
    .\Download_Scripts_SQL_Walkthrough.ps1 –DestDir 'C:\tempPythonSQL'
    ```
    
    如果您在 *DestDir* 中指定的資料夾不存在，PowerShell 指令碼就會加以建立。
    
    如果您收到錯誤，您可以暫時設定的 PowerShell 指令碼來執行原則**不受限制**僅適用於此逐步解說中，使用**略過**引數及範圍設定為目前的變更工作階段。 執行此命令不會導致設定變更。
    
    `Set\-ExecutionPolicy Bypass \-Scope Process`

3. 按照網際網路的連線速度，下載可能需要一些時間。 當所有檔案皆已下載時，PowerShell 指令碼會開啟  *DestDir*所指定的資料夾。 在 PowerShell 命令提示字元中，執行下列命令，並檢閱已下載的檔案。

    ```
    ls
    ```
**結果：**

![PowerShell 指令碼下載的檔案清單](media/sqldev-python-filelist.png "PowerShell 指令碼下載的檔案清單")

## <a name="next-step"></a>下一個步驟

[步驟 2︰使用 PowerShell 將資料匯入 SQL Server](sqldev-py2-import-data-to-sql-server-using-powershell.md)

## <a name="previous-step"></a>上一個步驟

[資料庫內 Python 分析 SQL 開發人員](sqldev-in-database-python-for-sql-developers.md)

## <a name="see-also"></a>另請參閱

[使用 Python 的機器學習服務](../python/sql-server-python-services.md)



