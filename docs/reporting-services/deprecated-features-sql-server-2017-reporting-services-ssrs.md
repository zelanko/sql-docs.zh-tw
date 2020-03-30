---
title: SQL Server 2017 Reporting Services 中已淘汰的功能 | Microsoft Docs
description: 本文描述下一版 SQL Server Reporting Services 中即將淘汰的功能。
ms.date: 11/20/2019
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
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: d8fe51ce9d86688669e84ad866ad9f5e6da075e8
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "74320312"
---
# <a name="deprecated-features-in-sql-server-2017-reporting-services"></a>SQL Server 2017 Reporting Services 中已淘汰的功能

[!INCLUDE [ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2017](../includes/ssrs-appliesto-2017.md)] [!INCLUDE [ssrs-appliesto-not-pbirs](../includes/ssrs-appliesto-not-pbirs.md)]

當我們將功能標示為已淘汰時，表示：

- 功能僅限維護模式。 我們不會再進行任何新的變更，包括與新功能互通性的相關變更。
- 為更容易升級，我們盡量不移除未來版本中已淘汰的功能。 不過，在極少數的情況下，如果該功能限制未來創新，我們可能會選擇從 Reporting Services 中永久移除這些功能。
- 我們不建議在新開發工作中使用已淘汰的功能。

## <a name="features-deprecated-in-the-next-version-of-sql-server"></a>下一版的 SQL Server 中已淘汰的功能

下列 SQL Server 2017 Reporting Services 功能將在下一版的 SQL Server 中淘汰。 請勿在新的開發工作中使用這些功能，並且儘速修改使用這些功能的應用程式。

> [!NOTE]
> 這份清單與 SQL Server 2016 Reporting Services (13.x) 清單完全相同。 SQL Server 2017 Reporting Services (14.x) 未宣告任何新的已淘汰或已停止功能。


| **類別目錄** | **已淘汰的功能** | **取代** |
| --- | --- | --- |
| 報表伺服器 | HTML 4.0 轉譯器。 | HTML 5 轉譯器 |

## <a name="see-also"></a>另請參閱

[SQL Server Reporting Services (SSRS) 中已停止的功能](discontinued-functionality-to-sql-server-reporting-services-in-sql-server.md)

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](https://go.microsoft.com/fwlink/?LinkId=620231)
