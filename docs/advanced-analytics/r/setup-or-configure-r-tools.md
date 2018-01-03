---
title: "SQL Server 安裝程式所含的 R 工具 |Microsoft 文件"
ms.custom: 
ms.date: 10/31/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7c04ae30-d391-4369-9742-d2b275e14c0d
caps.latest.revision: "9"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 9090313eed0997ea03329338c358825932dd8379
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/20/2017
---
# <a name="r-tools-included-with-sql-server-setup"></a>SQL Server 安裝程式所含的 R 工具

當您安裝 R 與 SQL Server 時，您會收到相同與任何已安裝的 R 工具**基底**R，例如 RGui、 Rterm，以及其他等等的安裝。 因此技術上來說，您必須開發和測試 R 程式碼所需的所有工具。

本主題列出安裝所隨附的工具。

> [!TIP]
> 
> 一般來說，這是您更輕鬆地偵錯和測試 R 程式碼所使用的專用的開發環境。 您會發現您更輕鬆地在 SQL Server 中執行 R 程式碼，如果您事先在中進行測試外部工具，使您可以讀取詳細的錯誤訊息和偵錯方案。
> 
> 請參閱本文章清單免費工具，您可以用來開發 R 解決方案，以及如何設定它們使用 SQL Server:[資料科學用戶端設定](set-up-a-data-science-client.md)

**適用於：** SQL Server 2016 R 服務 （資料庫） 和 Microsoft R Server （獨立）;SQL Server 2017 機器學習服務 （資料庫） 和機器學習伺服器 （獨立）

## <a name="r-tools-included-with-installation"></a>隨附安裝的 R 工具

下列標準的 R 工具隨附的*基底安裝*，並因此預設會安裝。

+ **RTerm**： 命令列的終端機執行 R 指令碼

+ **RGui.exe**：R 的簡單互動式編輯器。RGui.exe 和 RTerm 的命令列引數相同。

+ **RScript**：以批次模式執行 R 指令碼的命令列工具。

若要尋找這些工具，決定當您設定 SQL Server 或獨立機器學習功能已安裝的 R 程式庫。 比方說，在預設安裝中，R 工具都在這些資料夾位於：

+ SQL Server 2016 R Services:`~\Program Files\Microsoft SQL Server\MSSQL13.<instancename>\R_SERVICES\bin\x64`
+ Microsoft R Server 的獨立：`~\Program Files\Microsoft R\R_SERVER\bin\x64`
+ SQL Server 2017 機器學習服務：`~\Program Files\Microsoft SQL Server\MSSQL14.<instancename>\R_SERVICES\bin\x64`
+ 機器學習服務伺服器 （獨立）：`~\Program Files\Microsoft\ML Server\R_SERVER\bin\x64`

如果您需要協助的 R 工具，直接開啟**RGui**，按一下 **協助**，然後選取其中一個選項。

## <a name="introducing-microsoft-r-client"></a>介紹 Microsoft R 用戶端

Microsoft R 用戶端是免費下載，可讓您存取以供開發使用 RevoScaleR 封裝。 安裝 R 用戶端，您可以建立可以在所有支援的計算內容，包括 SQL Server 資料庫中的分析，以及 Hadoop、 Spark 或使用機器學習伺服器 Linux 上的分散式 R 運算執行的 R 解決方案。

如果您已經安裝不同的 R 開發環境，例如 RStudio，務必要使用的程式庫和 Microsoft R 用戶端所提供的可執行檔的環境重新設定。 藉由讓您可以使用 RevoScaleR 封裝中，所有的功能但效能會受到限制。

如需詳細資訊，請參閱[什麼是 Microsoft R 用戶端？](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client)
