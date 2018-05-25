---
title: 使用 SQL Server 機器學習服務上安裝 R 封裝的 T-SQL （建立外部程式庫） |Microsoft 文件
description: 將新的 R 封裝加入至 SQL Server 2017 機器學習服務 （資料庫）
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/20/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: bbc1adf4868cbfbd02afe5cae3a38fd6223e2d4d
ms.sourcegitcommit: b5ab9f3a55800b0ccd7e16997f4cd6184b4995f9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2018
---
# <a name="use-t-sql-create-external-library-to-install-r-packages-on-sql-server-2017-machine-learning-services"></a>使用 SQL Server 2017 機器學習服務上安裝 R 封裝的 T-SQL （建立外部程式庫）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文說明如何安裝新的 R 封裝在已啟用機器學習的 SQL Server 執行個體。 有多個從選擇的方法。 這種方法最適合的伺服器系統管理員不熟悉。

**適用於：**  [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

[建立外部程式庫](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql)陳述式會讓您能夠加入封裝一組特定資料庫或執行個體而不需執行 R 或直接 Python 程式碼。 不過，此方法需要封裝準備和其他資料庫的權限。

+ 所有封裝必須是可當做本機的 zip 檔案，而不是視需要從網際網路下載。

+ 必須由名稱和版本，所有相依性，並將其併入 zip 檔案。 如果封裝未提供，包括下游封裝相依性所需，陳述式將會失敗。 

+ 您必須在資料庫上的必要權限。 如需詳細資訊，請參閱[建立外部程式庫](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql)。

## <a name="download-packages-in-archive-format"></a>下載封裝封存格式

如果您要安裝在單一封裝，請下載 zip 格式的封裝。

如果封裝需要任何其他封裝，您必須驗證所需的封裝是否可用。 您可以使用 miniCRAN 來分析目標的封裝，並識別所有相依性。 我們建議您使用[ **miniCRAN** ](create-a-local-package-repository-using-minicran.md)或[ **igraph** ](http://igraph.org/r/)分析封裝相依性。 安裝的封裝或封裝的相依性版本錯誤也可能導致陳述式失敗。 

## <a name="copy-the-file-to-a-local-folder"></a>將檔案複製到本機資料夾

將複製 zip 壓縮的檔案包含所有的封裝，以在伺服器上的本機資料夾。 如果您在伺服器上沒有存取檔案系統，您也可以傳遞完整的封裝為變數，使用一種二進位格式。 如需詳細資訊，請參閱[建立外部程式庫](../../t-sql/statements/create-external-library-transact-sql.md)。

## <a name="run-the-statement-to-upload-packages"></a>執行陳述式上, 傳封裝

開啟**查詢**視窗中，使用具有系統管理權限的帳戶。

執行 T-SQL 陳述式`CREATE EXTERNAL LIBRARY`上傳到資料庫的 zip 壓縮的封裝集合。

    For example, the following statement names as the package source a miniCRAN repository containing the **randomForest** package, together with its dependencies. 

    ```R
    CREATE EXTERNAL LIBRARY randomForest
    FROM (CONTENT = 'C:\Temp\Rpackages\randomForest_4.6-12.zip')
    WITH (LANGUAGE = 'R');
    ```

    You cannot use an arbitrary name; the external library name must have the same name that you expect to use when loading or calling the package.

## <a name="verify-package-installation"></a>確認封裝安裝

如果已成功建立文件庫，您可以在 SQL Server 中，執行封裝，藉由呼叫預存程序。
    
    ```SQL
    EXEC sp_execute_external_script
    @language =N'R',
    @script=N'
    library(randomForest)'
    ```

