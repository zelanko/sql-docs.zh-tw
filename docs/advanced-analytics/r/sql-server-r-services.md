---
title: SQL Server 2016 中的 R Services
description: SQL Server 中的 r, 適用于關聯式資料的整合 R 工作, 包括資料科學和統計模型化、預測性分析、資料視覺效果等等。
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/10/2018
ms.topic: overview
author: dphansen
ms.author: davidph
monikerRange: =sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: e849140125ba39c7c1d8601c5ef32880a9d633ac
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/19/2019
ms.locfileid: "68344842"
---
# <a name="r-services-in-sql-server-2016"></a>SQL Server 2016 中的 R Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

R Services 是 SQL Server 2016 資料庫引擎實例的附加元件, 可用來在 SQL Server 上執行 R 程式碼和函式。 程式碼會在擴充性架構中執行, 並與核心引擎進程隔離, 但可完全提供給關聯式資料做為預存程式、包含 R 語句的 T-sql 腳本, 或當做包含 T-sql 的 R 程式碼。 

R 服務包含 R 的基底散發, 與 Microsoft 的企業 R 套件重迭, 因此您可以在多個核心上載入和處理大量資料, 並將結果匯總成單一合併輸出。 Microsoft 的 R 函式和演算法都是針對規模和公用程式而設計: 提供預測性分析、統計模型、資料視覺效果, 以及設計商務服務器產品中的最先進機器學習演算法受 Microsoft 支援。 

R 程式庫包含[**RevoScaleR**](ref-r-revoscaler.md)、 [**MicrosoftML (r)** ](ref-r-microsoftml.md)及其他專案。 由於 R 服務已與資料庫引擎整合, 因此您可以保持接近資料的分析, 並消除與資料移動相關聯的成本和安全性風險。

> [!Note]
> R 服務已在 SQL Server 2017 和更新版本中重新命名, 以[SQL Server Machine Learning 服務](../what-is-sql-server-machine-learning.md), 以反映 Python 的新增。

## <a name="components"></a>元件

SQL Server 2016 僅限 R。 下表描述 SQL Server 2016 中的功能。

| 元件 | 描述 |
|-----------|-------------|
| SQL Server Launchpad 服務 | 管理外部 R 執行時間和 SQL Server 實例之間通訊的服務。 |
| R 套件 | [**RevoScaleR**](ref-r-revoscaler.md)是可調整 R 的主要程式庫。此程式庫中的函式是最廣泛使用的功能之一。 在這些程式庫中可找到資料轉換和操作、統計摘要、視覺效果, 以及許多形式的模型化和分析。 此外, 這些程式庫中的函式會自動將工作負載分散到可用的核心, 以進行平行處理, 並且能夠處理由計算引擎協調和管理的資料區塊。  <br/>[**MicrosoftML (R)** ](ref-r-microsoftml.md)新增機器學習演算法, 以建立文字分析、影像分析和情感分析的自訂模型。 <br/>[**sqlRUtils**](ref-r-sqlrutils.md)提供 helper 函式, 可將 R 腳本放入 t-sql 預存程式、向資料庫註冊預存程式, 以及從 R 開發環境執行預存程式。<br/>[**olapR**](ref-r-olapr.md)是用來在 R 中指定 MDX 查詢。|
| Microsoft R Open (MRO) | [**MRO**](https://mran.microsoft.com/open)是 Microsoft 的 R 開放原始碼散發。包含封裝和解譯器。 請一律使用安裝程式所安裝的 MRO 版本。 |
| R 工具 | R 主控台視窗和命令提示字元是 R 散發套件中的標準工具。  |
| R 範例和腳本 |  開放原始碼 R 和 RevoScaleR 套件包含內建的資料集, 讓您可以使用預先安裝的資料來建立和執行腳本 |
| R 中預先定型的模型 | 預先定型的模型是針對特定使用案例所建立, 並由 Microsoft 的資料科學工程團隊進行維護。 您可以使用您所提供的新資料輸入, 依實際情況使用預先定型的模型來對文字中的正負情感進行評分, 或偵測影像中的特徵。 這些模型會在 R Services 中執行, 但是無法透過 SQL Server 安裝程式安裝。 如需詳細資訊, 請參閱[在 SQL Server 上安裝預先定型的機器學習模型](../install/sql-pretrained-models-install.md)。 |

## <a name="using-r-services"></a>使用 R Services

開發人員和分析師通常會在本機 SQL Server 實例上執行程式碼。 藉由加入 Machine Learning 服務並啟用外部腳本執行, 您就能夠在 SQL Server 形式: 在預存程式中包裝腳本、在 SQL Server 資料表中儲存模型, 或在查詢中結合 T-sql 和 R 函數, 以執行 R 程式碼。

資料庫內分析最常見的方法是使用[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), 傳遞 R 腳本做為輸入參數。

傳統的用戶端-伺服器互動是另一種方法。 從任何具有 IDE 的用戶端工作站, 您都可以安裝[Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client), 然後撰寫程式碼, 將執行 (稱為*遠端計算內容*) 推送至遠端 SQL Server 的資料和作業。 

最後, 如果您使用[獨立伺服器](r-server-standalone.md)和開發人員版本, 您可以使用相同的程式庫和解譯器在用戶端工作站上建立解決方案, 然後在 SQL Server Machine Learning 服務 (資料庫內) 上部署生產環境程式碼。 

## <a name="how-to-get-started"></a>如何開始使用

從安裝程式開始, 將二進位檔附加至您最愛的開發工具, 並撰寫您的第一個腳本。

**步驟 1：** 安裝和設定軟體。 

+ [安裝 SQL Server 2016 R Services (資料庫內)](../install/sql-r-services-windows-install.md)

**步驟 2：** 使用下列其中一種教學課程來取得實際操作體驗:

+ [教學課程：瞭解使用 R 的資料庫內分析](../tutorials/sqldev-in-database-r-for-sql-developers.md)
+ [教學課程：使用 R 的端對端逐步解說](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)

**步驟 3：** 新增您最愛的 R 套件, 並搭配 Microsoft 提供的套件一起使用

+ [適用于 SQL Server 的 R 套件管理](install-additional-r-packages-on-sql-server.md)


## <a name="see-also"></a>另請參閱

 [安裝 SQL Server 2016 R 服務](../install/sql-r-services-windows-install.md)
