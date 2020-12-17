---
title: SQL Server 2019 Reporting Services 中已淘汰的功能 | Microsoft Docs
description: 本文說明下一版 SQL Server Reporting Services 中即將淘汰的 SQL Server 2019 Reporting Services 功能。
ms.date: 08/31/2020
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- Reporting Services, backward compatibility
- deprecated features [Reporting Services]
- HTML OWC rendering extension [Reporting Services]
- Report Server Web service, endpoints
ms.assetid: 3876c01e-f81d-4cce-9104-5106a8c369e6
author: maggiesMSFT
ms.author: maggies
monikerRange: '>= sql-server-ver15'
ms.openlocfilehash: d5f173bf7fa557a963a55b0a88a9dc48fae74a66
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97425203"
---
# <a name="deprecated-features-in-sql-server-2019-reporting-services"></a>SQL Server 2019 Reporting Services 中已淘汰的功能

[!INCLUDE [ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2019-and-later](../includes/ssrs-appliesto-2019-and-later.md)] [!INCLUDE [ssrs-appliesto-pbirs](../includes/ssrs-appliesto-pbirs.md)]

當我們將功能標示為已淘汰時，表示：

- 功能僅限維護模式。 我們不會再進行任何新的變更，包括與新功能互通性的相關變更。
- 為更容易升級，我們盡量不移除未來版本中已淘汰的功能。 不過，在極少數的情況下，如果該功能限制未來創新，我們可能會選擇從 Reporting Services 中永久移除這些功能。
- 我們不建議在新開發工作中使用已淘汰的功能。

**SQL Server 未來版本中已淘汰的功能**

SQL Server Reporting Services 在下一版的 SQL Server 中支援下列功能，但這些功能會在更新的版本中淘汰。 SQL Server 的特定版本尚未決定。

| **類別目錄** | **已淘汰的功能** | **取代** |
| --- | --- | --- |
| 報表伺服器 | 報表組件庫 | None |
| 報表伺服器 | 行動報表和行動報表發行工具 | Power BI 報表伺服器中的 Power BI 報表提供行動功能。 |
| 報表伺服器 | XLS 和 DOC 轉譯格式 | 可用和受支援的 XLSX 和 DOCX 格式。 |
| 報表伺服器 | Atom 資料摘要 | oData 摘要支援適用於 SSRS 和 Power BI 報表伺服器中的共用資料集。 |
| 報表伺服器 | 釘選到 Power BI | 編頁報表支援現已可直接在 Power BI 服務中取得。  |

## <a name="see-also"></a>另請參閱

[SQL Server 2019 Reporting Services (SSRS) 中已停止的功能](discontinued-functionality-sql-server-reporting-services-2019.md)

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](https://go.microsoft.com/fwlink/?LinkId=620231)
