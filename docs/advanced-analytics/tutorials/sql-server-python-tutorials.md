---
title: SQL Server Python 教學課程 |Microsoft 文件
titleSuffix: SQL Server
ms.custom: ''
ms.date: 03/06/2018
ms.reviewer: ''
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: tutorial
applies_to:
- SQL Server 2017
dev_langs:
- Python
ms.author: heidist
author: HeidiSteen
manager: cgronlun
ms.openlocfilehash: 690d27faac3fff53c72abc80690899117d8ea9ce
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/04/2018
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

   這一課將示範您如何執行程式碼從遠端的 Python 終端機中，使用 SQL Server 計算內容。 您應該熟悉的 Python 工具和環境。 範例程式碼所提供，會建立模型，使用**rxLinMod**，從新**revoscalepy**程式庫。 

+ [在資料庫 Python 分析的 SQL 開發人員](sqldev-in-database-python-for-sql-developers.md)

    本端對端逐步解說示範如何建置完整的 Python 解決方案使用 T-SQL 預存程序的程序。 所有的 Python 程式碼包含項目。


## <a name="python-samples"></a>Python 範例

這些範例和 SQL Server 開發團隊所提供的示範反白顯示您可以在真實世界應用程式中使用內嵌的分析方式。

+ [建置預測模型使用 Python 和 SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/)

  了解 ski 以租用方式佔用企業可能會使用機器學習來預測未來出租，它可以幫助商務計劃和人員，以符合未來的要求。

  > [!TIP]
  > 現在包含原生計分 Python 模型 ！

+ [執行客戶群集使用 Python 和 SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/customerclustering/)

    了解如何使用 Kmeans 演算法來執行不受監督的群集的客戶。

## <a name="bkmk_Prerequisites"></a>必要條件

若要使用這些教學課程，您必須擁有 SQL Server 2017，，您必須明確地安裝，然後啟用該功能，機器學習服務 （資料庫）。 

SQL Server 2017 支援 R 和 Python 語言，但兩者都不是安裝或預設為啟用。 執行 Python 需要啟用擴充性架構，並且必須 Python 選取為要安裝的語言。 

### <a name="post-installation-configuration-tips"></a>安裝後設定秘訣

執行 SQL Server 安裝程式之後，您可能需要執行一些額外的步驟，以確保 Python 和 SQL Server 進行通訊：

+ 執行啟用外部指令碼執行功能`sp_configure 'external scripts enabled', 1`。
+ 重新啟動伺服器。 
+ 開啟**服務**面板來檢查是否已啟動 [啟動列]。 
+ 請確定呼叫外部執行階段的服務具有必要權限。 如需詳細資訊，請參閱[啟用隱含的驗證](../r/add-sqlrusergroup-to-database.md)。
+ 開啟防火牆上的連接埠的 SQL Server，並啟用必要的網路通訊協定。
+ 請確定您的 SQL 登入或 Windows 使用者帳戶具有必要權限連接到伺服器，來讀取資料，並建立此範例所需的任何資料庫物件。

請參閱本文章的一些常見問題：[疑難排解機器學習服務](../machine-learning-troubleshooting-faq.md)

### <a name="resource-management"></a>資源管理

您可以在相同的電腦上安裝 R 和 Python，但同時執行，可能需要大量資源。 如果您收到 「 記憶體不足 」 錯誤，或是執行機器學習工作是主體想要使用的伺服器，您可以減少配置給資料庫引擎的記憶體數量。 如需詳細資訊，請參閱[管理及監視 SQL Server 中的 Python](../python/managing-and-monitoring-python-solutions.md)。

## <a name="see-also"></a>另請參閱

[適用於 SQL Server 的 R 教學課程](sql-server-r-tutorials.md)
