---
title: SQL Server 2016 中的 R Services |Microsoft Docs
description: SQL Server 服務的概觀介紹，R 支援的資料庫內分析
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/27/2018
ms.topic: overview
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 9be6cf7b38482673db0308b4680500dede313e09
ms.sourcegitcommit: e4e9f02b5c14f3bb66e19dec98f38c012275b92c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/28/2018
ms.locfileid: "43118336"
---
# <a name="r-services-in-sql-server-2016"></a>SQL Server 2016 中的 R Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server 2016 R Services 是 database engine 執行個體，用於 SQL Server 上執行 R 程式碼的附加元件。 與核心引擎處理序隔離，但預存程序、 T-SQL 指令碼包含 R 陳述式，或包含 T-SQL 的 R 程式碼的關聯式資料完全可供使用的擴充性架構中，執行程式碼。 

R Services 包含基底散發套件的 R，重疊與來自 Microsoft 的企業 R 套件，讓您可以載入和處理多個核心上大量的資料和彙總成單一的彙總輸出的結果。 Microsoft 的 R 函式和演算法設計成可調整和公用程式： 提供預測性分析、 統計模型、 資料視覺效果，與頂尖的機器學習演算法中設計商業 server 產品和Microsoft 支援。 

R 程式庫包含 RevoScaleR、 MicrosoftML 及其他。 因為 R Services 會與 database engine 整合，您可以讓分析貼近資料，並排除與移動資料相關聯的安全性風險與成本。

## <a name="components"></a>Components

SQL Server 2016 只是 R。 下表說明 SQL Server 2016 中的功能。

| 元件 | 描述 |
|-----------|-------------|
| SQL Server Launchpad 服務 | 管理外部 R 執行階段和 SQL Server 執行個體之間的通訊服務。 |
| R 套件 | [**RevoScaleR** ](revoscaler-overview.md)是主要的程式庫，此程式庫中的可調整 r 函數是使用最廣泛。 這些程式庫中找到資料轉換和操作、 統計摘要、 視覺化和模型化和分析的許多形式。 此外，這些程式庫中的函式會自動將工作負載分散到可用的核心進行平行處理，能夠協調及計算引擎所管理的資料區塊上運作。  <br/>[**MicrosoftML (R)** ](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)新增機器學習演算法來建立自訂文字分析、 影像分析和情緒分析模型。 <br/>[**sqlRUtils** ](generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md)提供 helper 函式將 R 指令碼放入 T-SQL 預存程序、 註冊預存程序使用資料庫時，以及從 R 開發環境執行預存程序。<br/>[**olapR** ](how-to-create-mdx-queries-using-olapr.md)用於指定 MDX 查詢|
| Microsoft R Open (MRO) | [**MRO** ](https://mran.microsoft.com/open)是 Microsoft 的開放原始碼散發套件的。會包含封裝和解譯器。 一律使用 MRO 安裝程式安裝的版本。 |
| R 工具 | R 主控台視窗和命令提示字元是標準的工具，在 R 散發。  |
| R 範例和指令碼 |  開放原始碼 R 和 RevoScaleR 套件包含內建的資料集，可讓您可以建立並使用預先安裝的資料執行指令碼 |
| 在 R 中預先定型的模型 | 預先定型的模型建立的特定使用案例，並由 Microsoft 的資料科學工程小組所維護。 您可以使用預先定型的模型，以-為評分正負面情感的文字，或在映像，使用您提供的新資料輸入中偵測功能。 模型在 R Services 中執行，但無法透過 SQL Server 安裝程式安裝。 如需詳細資訊，請參閱 <<c0> [ 安裝的預先定型的機器學習服務模型在 SQL Server 上的](../install/sql-pretrained-models-install.md)。 |

## <a name="how-to-get-started"></a>如何開始使用

啟動安裝程式、 將二進位檔附加至您最愛的開發工具和撰寫第一個指令碼。

**步驟 1:** 安裝及設定軟體。 

+ [安裝 SQL Server 2016 R Services （資料庫）](../install/sql-r-services-windows-install.md)

**步驟 2:** 獲得實際操作經驗，使用這些教學課程中的其中之一：

+ [教學課程： 了解使用 R 的資料庫內分析](../tutorials/sqldev-in-database-r-for-sql-developers.md)
+ [教學課程： 使用 R 的端對端逐步解說](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)

**步驟 3:** 新增您最愛的 R 封裝，並使用它們搭配 Microsoft 所提供的套件

+ [SQL Server 的 R 封裝管理](install-additional-r-packages-on-sql-server.md)


## <a name="see-also"></a>另請參閱

 [安裝 SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)
