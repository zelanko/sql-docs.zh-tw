---
title: "架構 |Microsoft 文件"
ms.custom: 
ms.date: 11/03/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: python
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 5ca823bc7094c77a31cfd3178294cd49a360d77a
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2018
---
# <a name="architecture-overview-for-machine-learning-services-with-python"></a>使用 Python 的機器學習服務的架構概觀
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本主題提供的 Python 與 SQL Server，包括支援外部指令碼執行的資料庫引擎和啟用 Python 與 SQL Server 的互通性的新元件中的安全性模型，元件的整合方式的概觀。 如需詳細資訊，請參閱連結的主題。

> [!IMPORTANT]
> 從 SQL Server 2017 CTP 2.0 Python 的支援。 此發行前版本功能會隨時變更。

## <a name="python-interoperability"></a>Python 互通性

SQL Server 機器學習服務 （資料庫） 安裝的 Python Anaconda 發佈和 Python 3.5 執行階段和解譯器。 這可確保接近完成與標準 Python 解決方案的相容性。 從 SQL Server，以確保不會影響資料庫作業，在個別的處理序中執行 Python。

如需 SQL server 使用 Python 互動的詳細資訊，請參閱[Python 互通性](../../advanced-analytics/python/python-interoperability.md)

## <a name="components-that-support-python-integration"></a>支援 Python 整合的元件

現在 SQL Server 2016 中引進的擴充性架構支援執行 Python 指令碼，透過加入新的語言特有的元件。 這些元件改善資料交換速度和壓縮，同時提供安全且高效能的平台執行外部指令碼。

如需詳細說明的元件，例如支援 Python，[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]和 PythonLauncher，請參閱[新元件](../../advanced-analytics/python/new-components-in-sql-server-to-support-python-integration.md)。

## <a name="security"></a>Security

在 SQL Server 處理序，以提供安全性和更高的管理性之外，執行 Python 工作。

所有工作都受 Windows 作業物件或 SQL Server 安全性都保護。 藉由強制執行 SQL Server 資料表、 資料庫和執行個體層級的安全性相容性界限內保留資料。 資料庫管理員可以控制誰能夠執行 Python 作業、 監視使用 Python 指令碼的使用者，並檢視所使用的資源。

如需詳細資訊，請參閱[Python 的安全性](../../advanced-analytics/python/security-overview-sql-server-python-services.md)

## <a name="resource-governance"></a>資源管理

在 SQL Server Enterprise Edition，您可以使用資源管理員來管理和監視資源使用的外部指令碼作業，包括 R 指令碼和 Python 指令碼。

如需詳細資訊，請參閱[資源管理針對 R](../../advanced-analytics/r/resource-governance-for-r-services.md)。

## <a name="next-steps"></a>後續的步驟

[執行 Python 使用 T-SQL](../tutorials/run-python-using-t-sql.md)
