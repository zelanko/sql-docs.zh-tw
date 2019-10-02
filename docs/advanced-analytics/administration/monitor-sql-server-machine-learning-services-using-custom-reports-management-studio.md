---
title: 使用 SSMS 中的自訂報表監視 Python 和 R 腳本執行
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/17/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 549cdcd35b939b2247b14817271e3d1063fab1e0
ms.sourcegitcommit: fd3e81c55745da5497858abccf8e1f26e3a7ea7d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2019
ms.locfileid: "71714392"
---
# <a name="monitor-python-and-r-script-execution-using-custom-reports-in-sql-server-management-studio"></a>使用 SQL Server Management Studio 中的自訂報表監視 Python 和 R 腳本執行
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

使用 SQL Server Management Studio （SSMS）中的自訂報表來監視外部腳本的執行（Python 和 R）、使用的資源、診斷問題，以及調整 SQL Server Machine Learning 服務中的效能。

在這些報告中, 您可以查看詳細資料, 例如:

- 作用中的 Python 或 R 會話
- 實例的配置設定
- 機器學習作業的執行統計資料
- R Services 的擴充事件
- 安裝在目前實例上的 Python 或 R 套件

本文說明如何安裝和使用針對 SQL Server Machine Learning 服務提供的自訂報表。

如需 SQL Server Management Studio 中報表的詳細資訊，請參閱[Management Studio 中的自訂報表](../../ssms/object/custom-reports-in-management-studio.md)。

## <a name="how-to-install-the-reports"></a>如何安裝報表

這些報表是使用 SQL Server Reporting Services 所設計，但可以直接從 SQL Server Management Studio 使用。 Reporting Services 不一定要安裝在您的 SQL Server 實例上。

若要使用這些報表，請遵循下列步驟：

1. 從 GitHub 下載適用于 SQL Server Machine Learning 服務的[SSMS 自訂報表](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/machine-learning-services/ssms-custom-reports)。

2. 將報表複製到 Management Studio

    1. 找到 SQL Server Management Studio 使用的自訂報表資料夾。 根據預設，自訂報表會儲存在此資料夾中 **（其中，** 使用者名稱是您的 Windows 使用者名稱）：

        `C:\Users\user_name\Documents\SQL Server Management Studio\Custom Reports`

       您也可以指定不同的資料夾，或建立子資料夾。

    2. 複製 *。您下載到 [自訂報告] 資料夾的 RDL 檔案。

3. 在 Management Studio 中執行報表

    1. 在 Management Studio 中，以滑鼠右鍵按一下要執行報表的執行個體 [資料庫] 節點。

    2. 依序按一下 [報表]及 [自訂報表]。

    3. 在 [開啟檔案] 對話方塊中，找出自訂報表資料夾。

    4. 選取下載的其中一個 RDL 檔案，再按一下 [開啟]。

## <a name="reports"></a>報表

[GitHub 中的 SSMS 自訂報表存放庫](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/machine-learning-services/ssms-custom-reports)包含下列報告：

| 報表 | 描述 |
|-|-|
| Active Sessions | 目前連線至 SQL Server 實例並執行 Python 或 R 腳本的使用者。 |
| 組態 | Python 或 R 執行時間 Machine Learning 服務和屬性的安裝設定。 |
| 設定實例 | 設定 Machine Learning 服務。 |
| 執行統計資料 | Machine Learning 服務的執行統計資料。 例如，您可以取得外部腳本執行總數和平行執行次數。 |
| 擴充事件 | 擴充事件，可讓您深入瞭解外部腳本的執行。 |
| Packages | 列出安裝在 SQL Server 實例及其屬性上的 R 或 Python 套件，例如 [版本] 和 [名稱]。 |
| 資源使用狀況 | 查看 CPU、記憶體、SQL Server 的 IO 耗用量，以及外部腳本的執行。 您也可以查看外部資源集區的記憶體設定。 |

## <a name="next-steps"></a>後續步驟

- [使用動態管理檢視（Dmv）監視 SQL Server Machine Learning 服務](monitor-sql-server-machine-learning-services-using-dynamic-management-views.md)
- [R Services 的擴充事件](../r/extended-events-for-sql-server-r-services.md)
