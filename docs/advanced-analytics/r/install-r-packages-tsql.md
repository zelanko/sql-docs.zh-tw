---
title: 使用 SQL Server 機器學習服務上安裝 R 封裝的 T-SQL （建立外部程式庫） |Microsoft 文件
description: 將新的 R 封裝加入至 SQL Server 2017 機器學習服務 （資料庫）
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/30/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 7a5a0c394e9a26244661a4ae712d20583c1f1c99
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2018
ms.locfileid: "34585480"
---
# <a name="use-t-sql-create-external-library-to-install-r-packages-on-sql-server-2017-machine-learning-services"></a>使用 SQL Server 2017 機器學習服務上安裝 R 封裝的 T-SQL （建立外部程式庫）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文說明如何在機器學習服務啟用的位置的 SQL Server 執行個體上安裝新的 R 封裝。 有多個從選擇的方法。 使用 T-SQL 最適用伺服器系統管理員不熟悉。

**適用於：**  [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

[建立外部程式庫](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql)陳述式會讓您能夠加入封裝一組特定資料庫或執行個體而不需執行 R 或直接 Python 程式碼。 不過，此方法需要封裝準備和其他資料庫的權限。

+ 所有封裝都必須都是可從本機 zip 檔案，而不是視需要從網際網路下載。

+ 必須由名稱和版本，所有相依性，並將其併入 zip 檔案。 如果封裝未提供，包括下游封裝相依性所需，陳述式將會失敗。 

+ 您必須是**db_owner**或擁有資料庫角色中建立外部程式庫的權限。 如需詳細資訊，請參閱[建立外部程式庫](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql)。

## <a name="download-packages-in-archive-format"></a>下載封裝封存格式

如果您要安裝在單一封裝，請下載 zip 格式的封裝。

很多常見安裝多個封裝，因為封裝相依性。 當封裝需要其他封裝時，您必須確認全都是在安裝期間相互存取。 我們建議[建立本機儲存機制](create-a-local-package-repository-using-minicran.md)使用[miniCRAN](http://andrie.github.io/miniCRAN/)組合一個完整封裝的集合，以及[igraph](http://igraph.org/r/)分析封裝相依性。 安裝封裝的版本錯誤或省略封裝相依性可能會導致建立外部程式庫陳述式失敗。 

## <a name="copy-the-file-to-a-local-folder"></a>將檔案複製到本機資料夾

將複製 zip 壓縮的檔案包含所有的封裝，以在伺服器上的本機資料夾。 如果您在伺服器上沒有存取檔案系統，您也可以傳遞完整的封裝為變數，使用一種二進位格式。 如需詳細資訊，請參閱[建立外部程式庫](../../t-sql/statements/create-external-library-transact-sql.md)。

## <a name="run-the-statement-to-upload-packages"></a>執行陳述式上, 傳封裝

開啟**查詢**視窗中，使用具有系統管理權限的帳戶。

執行 T-SQL 陳述式`CREATE EXTERNAL LIBRARY`上傳到資料庫的 zip 壓縮的封裝集合。

例如，下列陳述式做為封裝來源 miniCRAN 儲存機制含有名稱**randomForest**封裝，以及其相依性。 

```SQL
CREATE EXTERNAL LIBRARY randomForest
FROM (CONTENT = 'C:\Temp\Rpackages\randomForest_4.6-12.zip')
WITH (LANGUAGE = 'R');
```

您無法使用任意名稱。外部程式庫名稱都必須具有您預期時載入，或呼叫封裝所使用的相同名稱。

## <a name="verify-package-installation"></a>確認封裝安裝

如果已成功建立文件庫，您可以在 SQL Server 中，執行封裝，藉由呼叫預存程序。
    
```SQL
EXEC sp_execute_external_script
@language =N'R',
@script=N'library(randomForest)'
```

## <a name="see-also"></a>另請參閱

+ [取得封裝資訊](determine-which-packages-are-installed-on-sql-server.md)
+ [R 教學課程](../tutorials/sql-server-r-tutorials.md)
+ [使用說明指南](sql-server-machine-learning-tasks.md)