---
title: "SQL Server Python 教學課程 |Microsoft 文件"
ms.custom:
- SQL2016_New_Updated
ms.date: 09/19/2017
vapplies_to:
- SQL Server 2017
dev_langs:
- Python
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.openlocfilehash: 42a9339f5983eeef28250db7a384f37efd4dad9d
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2018
---
# <a name="sql-server-python-tutorials"></a>SQL Server Python 教學課程
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文提供教學課程和範例，示範如何使用 Python 與 SQL Server 2017 的清單。 透過這些範例和示範中，您將學習：

+ 如何從 T-SQL 執行 Python
+ 遠端和本機計算內容和您可以執行使用 SQL Server 電腦的 Python 程式碼的方式為何
+ 如何將 Python 程式碼包裝在預存程序
+ 最佳化 SQL 實際執行環境的 Python 程式碼
+ 內嵌在應用程式中的機器學習的真實世界案例

如需需求和安裝資訊，請參閱[必要條件](#bkmk_Prerequisites)。

## <a name="bkmk_pythontutorials"></a>Python 教學課程

+ [在 T-SQL 中執行 Python](run-python-using-t-sql.md)

   了解如何在 T-SQL、 使用 pioneered SQL Server 2016 中的擴充性機制中呼叫 Python 的基本概念。

+ [建立機器學習中使用 revoscalepy Python 模型](use-python-revoscalepy-to-create-model.md)

   您將建立模型，使用**rxLinMod**，從新**revoscalepy**程式庫。 您將會啟動遠端的 Python 終端機中的程式碼，但模型，就會進行 SQL Server 計算內容中。

+ [在資料庫 Python 分析的 SQL 開發人員](sqldev-in-database-python-for-sql-developers.md)

  新增！ 建置完整的 Python 解決方案使用 T-SQL 預存程序。 所有的 Python 程式碼包含項目。

+ [部署和使用 Python 模型](..\python\publish-consume-python-code.md)

  了解如何部署使用 Microsoft Machine Learning 伺服器的最新版本的 Python 模型。

## <a name="python-samples"></a>Python 範例

這些範例和 SQL Server 開發團隊所提供的示範反白顯示您可以在真實世界應用程式中使用內嵌的分析方式。

+ [建置預測模型使用 Python 和 SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/)

  了解 ski 以租用方式佔用企業可能會使用機器學習來預測未來出租，它可以幫助商務計劃和人員，以符合未來的要求。

  > [!TIP]
  > 現在包含原生計分 Python 模型 ！

+ [執行客戶群集使用 Python 和 SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/customerclustering/)

    了解如何使用 Kmeans 演算法來執行不受監督的群集的客戶。

## <a name="bkmk_Prerequisites"></a>必要條件

若要使用這些教學課程，您必須已安裝 SQL Server 2017 機器學習服務 （資料庫）。 SQL Server 2017 支援 R 或 Python。 不過，您必須安裝支援機器學習的擴充性架構，並選取要安裝的語言為 Python。 您可以在同一部電腦上安裝 R 和 Python。

> [!NOTE]
>
> Python 支援是 SQL Server 2017 中的新功能，而且需要 CTP 2.0 或更新版本。 雖然此功能是發行前版本並不支援實際執行環境中，我們邀請您現在就試試看，並傳送意見反應。

**SQL Server 2017**

執行 SQL Server 安裝程式，別忘了下列重要步驟：

+ 執行啟用外部指令碼執行功能`sp_configure 'external scripts enabled', 1`。
+ 重新啟動伺服器。
+ 請確定呼叫外部執行階段的服務具有必要權限。
+ 請確定您的 SQL 登入或 Windows 使用者帳戶具有必要權限連接到伺服器，來讀取資料，並建立此範例所需的任何資料庫物件。

如果您遇到問題，請參閱本文章的一些常見問題：[疑難排解機器學習服務](../machine-learning-troubleshooting-faq.md)

## <a name="see-also"></a>另請參閱

[適用於 SQL Server 的 R 教學課程](sql-server-r-tutorials.md)
