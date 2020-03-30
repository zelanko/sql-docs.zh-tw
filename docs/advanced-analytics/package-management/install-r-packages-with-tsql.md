---
title: 使用 T-SQL (CREATE EXTERNAL LIBRARY) 來安裝 R 套件
description: 新增 R 套件至 SQL Server 2016 R Services 或 SQL Server Machine Learning Services (資料庫內)。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/20/2019
ms.topic: conceptual
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: =sql-server-2017||=sqlallproducts-allversions
ms.openlocfilehash: b19b2df1b39bcc88332d60f1389be12b32d7b921
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "74485263"
---
# <a name="use-t-sql-create-external-library-to-install-r-packages-on-sql-server"></a>使用 T-SQL (CREATE EXTERNAL LIBRARY) 在 SQL Server 上安裝 R 套件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

此文章說明如何在已啟用機器學習的 SQL Server 執行個體上安裝新的 R 套件。 有多種安裝方法可以選擇。 T-SQL 最適合不熟悉 R 的伺服器管理員採用。

**適用於：**  [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

[CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) 陳述式可讓您在不需要直接執行 R 或 Python 程式碼的情況下，將套件或套件集新增至執行個體或特定資料庫。 不過，此方法需要套件準備與其他資料庫權限。

+ 所有套件都必須以本機壓縮檔案 (而非以視需要從網際網路下載) 的形式提供。

+ 所有相依性都必須依名稱與版本來識別，並包含在 ZIP 檔案中。 如果必要套件無法使用 (包括下游套件相依性)，此陳述式會失敗。 

+ 您必須是 **db_owner** 或在資料庫角色中擁有 CREATE EXTERNAL LIBRARY 權限。 如需詳細資訊，請參閱 [CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql)。

## <a name="download-packages-in-archive-format"></a>以封存格式下載套件

如果您是要安裝單一套件，請以壓縮格式下載套件。

因為套件相依性的緣故，通常都會安裝多個套件。 當某個套件需要其他套件時，您必須在安裝期間確認它們彼此都能夠互相存取。 建議使用 [miniCRAN](create-a-local-package-repository-using-minicran.md) [建立本機存放庫](https://andrie.github.io/miniCRAN/)，以組合完整的套件集合，以及使用 [igraph](https://igraph.org/r/) 來分析套件相依性。 安裝錯誤的套件版本或省略套件相依性，可能會導致 CREATE EXTERNAL LIBRARY 陳述式失敗。 

## <a name="copy-the-file-to-a-local-folder"></a>將檔案複製到本機資料夾

將包含所有套件的壓縮檔案複製到伺服器上的本機資料夾。 如果您沒有權限可存取伺服器上的檔案系統，您也可以使用二進位格式，以變數形式傳遞完整套件。 如需詳細資訊，請參閱 [CREATE EXTERNAL LIBRARY](../../t-sql/statements/create-external-library-transact-sql.md)。

## <a name="run-the-statement-to-upload-packages"></a>執行陳述式以上傳套件

使用具備系統管理權限的帳戶開啟 [查詢]  視窗。

執行 T-SQL 陳述式 `CREATE EXTERNAL LIBRARY`，將壓縮的套件集合上傳至資料庫。

例如，下列陳述式會將包含 **randomForest** 套件的 miniCRAN 存放庫當做套件來源，連同其相依性一起命名。 

```sql
CREATE EXTERNAL LIBRARY randomForest
FROM (CONTENT = 'C:\Temp\Rpackages\randomForest_4.6-12.zip')
WITH (LANGUAGE = 'R');
```

您不能使用任意名稱；外部程式庫的名稱必須與您在載入或呼叫套件時預期使用的名稱相同。

## <a name="verify-package-installation"></a>驗證套件安裝

如果已成功建立程式庫，您就可以在 SQL Server 中，透過在預存程序內部呼叫套件來加以執行。
    
```sql
EXEC sp_execute_external_script
@language =N'R',
@script=N'library(randomForest)'
```

## <a name="see-also"></a>另請參閱

+ [取得 R 套件資訊](r-package-information.md)
+ [R 教學課程](../tutorials/sql-server-r-tutorials.md)