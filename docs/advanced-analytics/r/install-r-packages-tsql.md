---
title: 使用 T-sql (建立外部程式庫) 來安裝 R 套件
description: 將新的 R 封裝新增至 SQL Server 2016 R Services 或 SQL Server 2017 Machine Learning Services (資料庫內)。
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/12/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 80af3f93eb84c7b78c5cb1e5395175501931e24c
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470082"
---
# <a name="use-t-sql-create-external-library-to-install-r-packages-on-sql-server"></a>使用 T-sql (建立外部程式庫) 在 SQL Server 上安裝 R 套件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文說明如何在已啟用機器學習的 SQL Server 實例上安裝新的 R 封裝。 有多種方法可供選擇。 使用 T-sql 最適用于不熟悉 R 的伺服器管理員。

**適用物件:** [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)]  [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

[CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql)語句可讓您將封裝或封裝集新增至實例或特定資料庫, 而不需要直接執行 R 或 Python 程式碼。 不過, 此方法需要封裝準備和其他資料庫許可權。

+ 所有套件都必須以本機壓縮檔案的形式提供, 而不是從網際網路視需要下載。

+ 所有相依性都必須以名稱和版本來識別, 並包含在 zip 檔案中。 如果必要的套件無法使用, 則語句會失敗, 包括下游封裝相依性。 

+ 您必須是**db_owner**或擁有資料庫角色的 CREATE EXTERNAL LIBRARY 許可權。 如需詳細資訊, 請參閱[建立外部程式庫](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql)。

## <a name="download-packages-in-archive-format"></a>下載封存格式的套件

如果您要安裝單一套件, 請以壓縮格式下載套件。

因為套件相依性的緣故, 安裝多個套件是比較常見的方式。 當封裝需要其他套件時, 您必須在安裝期間確認彼此都可存取。 我們建議使用[miniCRAN](https://andrie.github.io/miniCRAN/)來[建立本機存放庫](create-a-local-package-repository-using-minicran.md), 以組合封裝的完整集合, 以及用來分析封裝相依性的[igraph](https://igraph.org/r/) 。 安裝錯誤的封裝版本或省略封裝相依性可能會導致 CREATE EXTERNAL LIBRARY 語句失敗。 

## <a name="copy-the-file-to-a-local-folder"></a>將檔案複製到本機資料夾

將包含所有封裝的 zip 壓縮檔案複製到伺服器上的本機資料夾。 如果您無法存取伺服器上的檔案系統, 您也可以使用二進位格式, 以變數的形式傳遞完整的封裝。 如需詳細資訊, 請參閱[建立外部程式庫](../../t-sql/statements/create-external-library-transact-sql.md)。

## <a name="run-the-statement-to-upload-packages"></a>執行語句來上傳封裝

使用具有系統管理許可權的帳戶開啟**查詢**視窗。

執行 t-sql 語句`CREATE EXTERNAL LIBRARY` , 將壓縮的封裝集合上傳至資料庫。

例如, 下列語句會將包含**randomForest**套件的 miniCRAN 存放庫名稱連同其相依性, 當做封裝來源。 

```sql
CREATE EXTERNAL LIBRARY randomForest
FROM (CONTENT = 'C:\Temp\Rpackages\randomForest_4.6-12.zip')
WITH (LANGUAGE = 'R');
```

您不能使用任意名稱;外部程式庫名稱必須具有您在載入或呼叫封裝時預期使用的相同名稱。

## <a name="verify-package-installation"></a>確認套件安裝

如果已成功建立程式庫, 您可以在 SQL Server 中執行封裝, 方法是在預存程式內呼叫它。
    
```sql
EXEC sp_execute_external_script
@language =N'R',
@script=N'library(randomForest)'
```

## <a name="see-also"></a>另請參閱

+ [取得封裝資訊](../package-management/installed-package-information.md)
+ [R 教學課程](../tutorials/sql-server-r-tutorials.md)
