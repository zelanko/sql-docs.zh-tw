---
title: "機器學習服務使用 Python |Microsoft 文件"
ms.date: 11/03/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: python
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ba1dea65-40ea-484a-b767-53680c954934
caps.latest.revision: "38"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: f1c4fa70a8466dc34793f0d90d9c67aae4e3dd63
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/20/2017
---
# <a name="machine-learning-services-with-python"></a>使用 Python 的機器學習服務

Python 是機器的一種語言，提供了相當大的彈性而且各種不同學習工作的功能。 For Python 開放原始碼程式庫包含數個平台，可自訂的類神經網路，以及常用的程式庫進行自然語言處理。 現在，在 SQL Server 2017 CTP 2.0 和更新版本可以支援此廣泛使用的語言。

因為與整合 Python[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫引擎，您可以讓分析資料並不需要成本和移動資料相關聯的安全性風險。  您可以部署使用方便且熟悉的工具，例如 Visual Studio 的 Python 為基礎的機器學習解決方案。 生產應用程式可以取得模型的預測或視覺效果的 Python 3.5 執行階段，只需呼叫 T-SQL 預存程序。

此版本包含 Python，以及新 Anaconda 發佈[revoscalepy](../python/what-is-revoscalepy.md)程式庫，以改善的小數位數和您的機器學習解決方案的效能。

您可以安裝您要開始使用 Python 透過 SQL Server 2017 安裝程式的所有項目：

+ **機器學習服務 （資料庫）：**安裝這項功能，以及 SQL Server 資料庫引擎，以啟用安全執行 Python 指令碼上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]電腦。
  
     當您選取這項功能，擴充功能會安裝在資料庫引擎可支援執行 Python 指令碼，並建立新的服務時，[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]來管理 Python 執行階段之間的通訊和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體。

+ **機器學習伺服器 （獨立）：**如果您不需要 SQL Server 整合，安裝才能取得分散式的機器學習的 Python 和 R 支援這項功能。 您也可以部署為 web 服務 Python 方案，使用**mrsdeploy**。
  
     請勿執行 SQL Server 機器學習服務在相同電腦上安裝此功能。


## <a name="additional-resources"></a>其他資源

[設定 Python 機器學習服務資料庫](setup-python-machine-learning-services.md)

[Python 教學課程](../tutorials/sql-server-python-tutorials.md)
