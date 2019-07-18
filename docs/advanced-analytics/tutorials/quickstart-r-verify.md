---
title: 驗證 R 的快速入門會存在於 SQL Server
description: 驗證 R 和 Machine Learning 服務存在於 SQL Server 的快速入門。
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
ms.openlocfilehash: f294f5f12e3efd734d1e54ace3041702c39d390a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67961969"
---
# <a name="quickstart-verify-r-exists-in-sql-server"></a>快速入門：驗證 R 存在於 SQL Server 中 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server 包含內建的 SQL Server 資料的資料科學分析的 R 語言支援。 您的 R 指令碼可以包含開放原始碼 R 函數，第三方的 R 程式庫或內建的 Microsoft R 程式庫這類[RevoScaleR](../r/revoscaler-overview.md)進行大規模的預測性分析。

執行指令碼是透過預存程序，使用下列其中一個方法：

+ 內建[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)預存程序，將 R 指令碼中的傳遞做為輸入參數。
+ 換行中的 R 指令碼[之自訂預存程序](sqldev-in-database-r-for-sql-developers.md)您所建立。

在本快速入門中，您會確認[SQL Server 2017 Machine Learning 服務](../what-is-sql-server-machine-learning.md)或是[SQL Server 2016 R Services](../r/sql-server-r-services.md)已安裝和設定。

## <a name="prerequisites"></a>先決條件

這個練習需要存取 SQL server 執行個體與其中一個已安裝下列項目：

+ [SQL Server 2017 Machine Learning 服務](../install/sql-machine-learning-services-windows-install.md)，與安裝的 R 語言
+ [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)

您的 SQL Server 執行個體可位於 Azure 虛擬機器或內部部署。 要小心，外部指令碼功能預設為停用，因此您可能需要[啟用外部指令碼](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature)，並確認**SQL Server Launchpad 服務**開始之前執行。

您也需要工具來執行 SQL 查詢。 您可以執行 R 指令碼使用的任何資料庫管理，或查詢工具，只要它可以連線到 SQL Server 執行個體，並執行 T-SQL 查詢或預存程序。 本快速入門會使用[SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms)。

## <a name="verify-r-exists"></a>請確認有 R

您可以確認您的 SQL Server 執行個體和已安裝的 R 版本，會啟用 Machine Learning 服務 （使用 R)。 請遵循下列步驟。

1. 開啟 SQL Server Management Studio 並連接到您的 SQL Server 執行個體。

2. 執行下列程式碼。 

    ```SQL
    EXECUTE sp_execute_external_script
    @language =N'R',
    @script=N'print(version)';
    GO
    ```

3. R`print`函式會傳回的版本**訊息**視窗。 在下列範例輸出中，您所見，SQL Server 在此情況下會有 R 3.3.3 安裝的版本。

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

如果您收到任何錯誤，此查詢，排除任何安裝問題。 若要啟用外部程式碼程式庫需要後續安裝設定。 請參閱[安裝 SQL Server 2017 Machine Learning 服務](../install/sql-machine-learning-services-windows-install.md)或是[安裝 SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)。 同樣地，請確定 Launchpad 服務正在執行。

根據您的環境，您可能需要啟用 R 背景工作帳戶以連線到 SQL Server、安裝額外的網路程式庫、啟用遠端程式碼執行，或在一切已設定完畢後重新啟動執行個體。 如需詳細資訊，請參閱 < [R Services 安裝和升級常見問題集](../r/upgrade-and-installation-faq-sql-server-r-services.md)。

## <a name="list-r-packages"></a>列出 R 套件

Microsoft 提供一些預先安裝在您的 SQL Server 執行個體的 使用機器學習服務的 R 套件。 若要查看清單中的哪些 R 套件安裝，包括版本、 相依性、 授權和程式庫路徑資訊，請遵循下列步驟。

1. 在您的 SQL Server 執行個體上執行下列指令碼。

    ```SQL
    EXECUTE sp_execute_external_script @language = N'R'
    , @script = N'
    OutputDataSet <- data.frame(installed.packages()[,c("Package", "Version", "Depends", "License", "LibPath")]);'
    WITH result sets((Package NVARCHAR(255), Version NVARCHAR(100), Depends NVARCHAR(4000)
        , License NVARCHAR(1000), LibPath NVARCHAR(2000)));
    ```

2. 輸出是從`installed.packages()`在 R 中並傳回結果集。

    **結果**

    ![在 R 中安裝套件](./media/rsql-installed-packages.png)

## <a name="next-steps"></a>後續步驟

現在您已確認您的執行個體已準備好使用 R，看看基本的 R 互動。

> [!div class="nextstepaction"]
> [快速入門：SQL Server 中的"Hello world"R 指令碼](quickstart-r-run-using-tsql.md)
