---
title: SQL Server 中存在驗證 R 的快速入門
description: 驗證 SQL Server 中是否有 R 和 Machine Learning 服務的快速入門。
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
ms.openlocfilehash: 951ffc07a32434b2f8d333140445f12c2971b811
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470621"
---
# <a name="quickstart-verify-r-exists-in-sql-server"></a>快速入門：驗證 R 存在於 SQL Server 中 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

SQL Server 包括對常駐 SQL Server 資料進行資料科學分析的 R 語言支援。 您的 R 腳本可以包含開放原始碼 R 函式、協力廠商 R 程式庫, 或內建的 Microsoft R 程式庫 (例如[RevoScaleR](../r/revoscaler-overview.md) ), 以進行大規模的預測性分析。

腳本執行是透過預存程式, 使用下列其中一種方法:

+ 內建的[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)預存程式, 以輸入參數的形式傳遞 R 腳本。
+ 將 R 腳本包裝在您建立的[自訂預存](sqldev-in-database-r-for-sql-developers.md)程式中。

在本快速入門中, 您將確認已安裝並設定[SQL Server 2017 Machine Learning Services](../what-is-sql-server-machine-learning.md)或[SQL Server 2016 R Services](../r/sql-server-r-services.md) 。

## <a name="prerequisites"></a>先決條件

此練習需要使用下列其中一項已安裝的 SQL Server 實例的存取權:

+ 已安裝 R 語言的[SQL Server 2017 Machine Learning 服務](../install/sql-machine-learning-services-windows-install.md)
+ [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)

您的 SQL Server 實例可以位於 Azure 虛擬機器或內部部署中。 請注意, 預設會停用外部腳本功能, 因此您可能需要[啟用外部腳本](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature), 並在開始之前確認**SQL Server Launchpad 服務**正在執行。

您也需要用來執行 SQL 查詢的工具。 您可以使用任何資料庫管理或查詢工具來執行 R 腳本, 只要它可以連接到 SQL Server 實例, 並執行 T-SQL 查詢或預存程式即可。 本快速入門使用[SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms)。

## <a name="verify-r-exists"></a>驗證 R 是否存在

您可以確認已針對您的 SQL Server 實例和安裝的 R 版本啟用 Machine Learning 服務 (使用 R)。 請遵循下列步驟。

1. 開啟 SQL Server Management Studio, 並連接到您的 SQL Server 實例。

2. 執行下列程式碼。 

    ```SQL
    EXECUTE sp_execute_external_script
    @language =N'R',
    @script=N'print(version)';
    GO
    ```

3. R `print`函數會將版本傳回至 [**訊息**] 視窗。 在下面的範例輸出中, 您可以看到此案例中的 SQL Server 已安裝 R 版本3.3.3。

    **結果**

    ```text
    platform       x86_64-w64-mingw32          
    arch           x86_64                      
    os             mingw32                     
    system         x86_64, mingw32             
    status                                     
    major          3                           
    minor          3.3                         
    year           2017                        
    month          03                          
    day            06                          
    svn rev        72310                       
    language       R                           
    version.string R version 3.3.3 (2017-03-06)
    nickname       Another Canoe               
    ```

如果您收到此查詢的任何錯誤, 請排除任何安裝問題。 必須安裝後續設定, 才能啟用外部程式碼程式庫的使用。 請參閱[安裝 SQL Server 2017 Machine Learning 服務](../install/sql-machine-learning-services-windows-install.md)或[安裝 SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)。 同樣地, 請確定啟動列服務正在執行。

根據您的環境，您可能需要啟用 R 背景工作帳戶以連線到 SQL Server、安裝額外的網路程式庫、啟用遠端程式碼執行，或在一切已設定完畢後重新啟動執行個體。 如需詳細資訊, 請參閱[R Services 安裝和升級常見問題](../r/upgrade-and-installation-faq-sql-server-r-services.md)。

## <a name="list-r-packages"></a>列出 R 套件

Microsoft 會在您的 SQL Server 實例中, 使用 Machine Learning 服務預先安裝數個 R 套件。 若要查看已安裝的 R 套件清單 (包括版本、相依性、授權和程式庫路徑資訊), 請遵循下列步驟。

1. 在您的 SQL Server 實例上執行下列腳本。

    ```SQL
    EXECUTE sp_execute_external_script @language = N'R'
    , @script = N'
    OutputDataSet <- data.frame(installed.packages()[,c("Package", "Version", "Depends", "License", "LibPath")]);'
    WITH result sets((Package NVARCHAR(255), Version NVARCHAR(100), Depends NVARCHAR(4000)
        , License NVARCHAR(1000), LibPath NVARCHAR(2000)));
    ```

2. 輸出來自`installed.packages()`于 R 中的, 並以結果集的形式傳回。

    **結果**

    ![R 中已安裝的套件](./media/rsql-installed-packages.png)

## <a name="next-steps"></a>後續步驟

既然您已確認您的實例已準備好使用 R, 請仔細查看基本的 R 互動。

> [!div class="nextstepaction"]
> [入門SQL Server 中的 "Hello world" R 腳本](quickstart-r-run-using-tsql.md)
