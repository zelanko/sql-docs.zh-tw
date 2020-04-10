---
title: 使用自訂報表監視指令碼
description: 使用 SQL Server Management Studio (SSMS) 中的自訂報表來監視外部指令碼 (Python 與 R) 的執行、使用的資源、診斷問題，以及調整 SQL Server 機器學習服務中的效能。
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/17/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: dad4cebf8259241b85497a0ff894228d125e839b
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/04/2020
ms.locfileid: "81118891"
---
# <a name="monitor-python-and-r-script-execution-using-custom-reports-in-sql-server-management-studio"></a>使用 SQL Server Management Studio 中的自訂報表監視 Python 與 R 指令碼的執行
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

使用 SQL Server Management Studio (SSMS) 中的自訂報表來監視外部指令碼 (Python 與 R) 的執行、使用的資源、診斷問題，以及調整 SQL Server 機器學習服務中的效能。

在這些報表中，您可以查看如下詳細資料：

- 作用中的 Python 或 R 工作階段
- 執行個體的組態設定
- 機器學習作業的執行統計資料
- R Services 的擴充事件
- 目前的執行個體上安裝的 Python 或 R 套件

此文章說明如何安裝及使用 SQL Server 機器學習服務提供的自訂報表。

如需 SQL Server Management Studio 中報表的詳細資訊，請參閱 [Management Studio 中的自訂報表](../../ssms/object/custom-reports-in-management-studio.md)。

## <a name="how-to-install-the-reports"></a>如何安裝報表

報表是使用 SQL Server Reporting Services 設計而成，但可直接從 SQL Server Management Studio 使用。 您的 SQL Server 執行個體上不需要安裝 Reporting Services。

若要使用這些報表，請遵循下列步驟：

1. 從 GitHub 下載適用於 SQL Server 機器學習服務的 [SSMS 自訂報表](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/machine-learning-services/ssms-custom-reports)。

2. 將報表複製到 Management Studio

    1. 找到 SQL Server Management Studio 使用的自訂報表資料夾。 根據預設，自訂報表會儲存在此資料夾中 (其中 **user_name** 是您的 Windows 使用者名稱)：

        `C:\Users\user_name\Documents\SQL Server Management Studio\Custom Reports`

       您可以指定不同的資料夾，或建立子資料夾。

    2. 將您下載的 *.RDL 檔案複製到自訂報表資料夾。

3. 在 Management Studio 中執行自訂報表

    1. 在 Management Studio 中，以滑鼠右鍵按一下要執行報表的執行個體 [資料庫]  節點。

    2. 依序按一下 [報表]  及 [自訂報表]  。

    3. 在 [開啟檔案]  對話方塊中，找出自訂報表資料夾。

    4. 選取下載的其中一個 RDL 檔案，再按一下 [開啟]  。

## <a name="reports"></a>報表

[GitHub 中的 SSMS 自訂報表存放庫](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/machine-learning-services/ssms-custom-reports)包含下列報表：

| Report | 描述 |
|-|-|
| Active Sessions | 目前已連線到 SQL Server 執行個體並執行 Python 或 R 指令碼的使用者。 |
| 組態 | Python 或 R 執行階段機器學習服務與屬性的安裝設定。 |
| 設定執行個體 | 設定機器學習服務。 |
| 執行統計資料 | 機器學習服務的執行統計資料。 例如，您可以取得外部指令碼執行總數與平行執行數目。 |
| 擴充事件 | 可讓您取得外部指令碼執行見解的擴充事件。 |
| Packages | 列出 SQL Server 執行個體上安裝的 R 或 Python 套件以及其屬性，例如版本與名稱。 |
| 資源使用狀況 | 檢視 SQL Server 的 CPU、記憶體、 IO 耗用量，以及外部指令碼的執行。 您也可以檢視外部資源集區的記憶體設定。 |

## <a name="next-steps"></a>後續步驟

- [使用動態管理檢視 (DMV) 監視 SQL Server 機器學習服務](monitor-sql-server-machine-learning-services-using-dynamic-management-views.md)
- [使用 SQL Server 機器學習服務中的擴充事件來監視 Python 與 R 指令碼](extended-events.md)
