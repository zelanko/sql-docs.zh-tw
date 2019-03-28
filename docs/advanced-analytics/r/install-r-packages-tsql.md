---
title: 若要安裝 R 封裝-SQL Server Machine Learning 服務中使用 T-SQL （建立外部程式庫）
description: 將新的 R 套件新增至 SQL Server 2016 R Services 或 SQL Server 2017 Machine Learning 服務 （資料庫）。
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/30/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: b59f15ace1dc96af537486336e76a209f1c85da7
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58510269"
---
# <a name="use-t-sql-create-external-library-to-install-r-packages-on-sql-server"></a>SQL Server 上安裝 R 封裝中使用 T-SQL （建立外部程式庫）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

這篇文章說明如何啟用機器學習服務的位置的 SQL Server 執行個體上安裝新的 R 套件。 有多個可從中選擇的方法。 使用 T-SQL 最能配合伺服器管理員，他們不熟悉。

**適用於：**  [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

[CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql)陳述式可讓您加入的封裝或組封裝的執行個體或特定的資料庫而不需執行 R 或 Python 程式碼直接。 不過，此方法需要封裝準備和其他資料庫的權限。

+ 所有封裝都必須都是可以做為本機的 zip 壓縮檔案，而不是視需要從網際網路下載。

+ 所有相依性必須由名稱和版本，並包含 zip 檔案中。 如果必要的套件都無法使用，包括下游的套件相依性，陳述式將會失敗。 

+ 您必須是**db_owner**或資料庫角色中擁有 CREATE EXTERNAL LIBRARY 權限。 如需詳細資訊，請參閱 < [CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql)。

## <a name="download-packages-in-archive-format"></a>下載封存格式的封裝

如果您正在安裝單一封裝，請下載 zip 格式的封裝。

很多常見安裝多個封裝，因為套件相依性。 當封裝需要其他套件時，您必須確認所有人都是在安裝期間存取彼此。 我們建議[建立本機儲存機制](create-a-local-package-repository-using-minicran.md)使用[miniCRAN](https://andrie.github.io/miniCRAN/)組合一個完整封裝的集合，以及[igraph](https://igraph.org/r/)分析封裝的相依性。 安裝封裝的版本錯誤或省略套件相依性可能會導致 CREATE EXTERNAL LIBRARY 陳述式失敗。 

## <a name="copy-the-file-to-a-local-folder"></a>將檔案複製到本機資料夾

複製包含伺服器上的本機資料夾的所有套件的 zip 壓縮的檔案。 如果您沒有伺服器的檔案系統的存取權，您也可以傳遞完整的封裝為變數，使用一種二進位格式。 如需詳細資訊，請參閱 < [CREATE EXTERNAL LIBRARY](../../t-sql/statements/create-external-library-transact-sql.md)。

## <a name="run-the-statement-to-upload-packages"></a>執行陳述式，將套件上傳

開啟**查詢**視窗中，使用具有系統管理權限的帳戶。

執行 T-SQL 陳述式`CREATE EXTERNAL LIBRARY`上壓縮的封裝集合傳到資料庫。

例如，下列陳述式名稱作為套件來源包含 miniCRAN 儲存機制**randomForest**封裝，以及其相依性。 

```sql
CREATE EXTERNAL LIBRARY randomForest
FROM (CONTENT = 'C:\Temp\Rpackages\randomForest_4.6-12.zip')
WITH (LANGUAGE = 'R');
```

您無法使用任意名稱;外部程式庫名稱必須與您預期時載入，或呼叫封裝所要使用相同的名稱。

## <a name="verify-package-installation"></a>請確認套件安裝

如果成功建立文件庫，您可以在 SQL Server 中，執行封裝，藉由呼叫預存程序項目。
    
```sql
EXEC sp_execute_external_script
@language =N'R',
@script=N'library(randomForest)'
```

## <a name="see-also"></a>另請參閱

+ [取得封裝資訊](determine-which-packages-are-installed-on-sql-server.md)
+ [R 教學課程](../tutorials/sql-server-r-tutorials.md)
+ [使用說明指南](sql-server-machine-learning-tasks.md)