---
title: 關於 SQL Server Analysis Services |Microsoft Docs
ms.date: 12/05/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: overview
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b2cd892ad41beba2b5715b3a7186ae5e44bb7911
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63206362"
---
# <a name="about-sql-server-analysis-services"></a>關於 SQL Server Analysis Services

Analysis Services 是用於決策支援和商業分析的分析資料引擎。 它提供企業級語意資料模型報表和用戶端應用程式，例如 Power BI、 Excel、 Reporting Services 報表和其他資料視覺效果工具。

一般工作流程包含在 Visual Studio 中建立表格式或多維度資料模型專案、 將模型部署為資料庫的伺服器執行個體、 設定週期性的資料處理和指派權限以允許由使用者進行資料存取。 準備就緒時，就可以存取語意資料模型支援 Analysis Services 做為資料來源的用戶端應用程式。

Analysis Services 會在兩個不同的平台：

**Azure Analysis Services** -支援 1200年和更高的相容性層級的表格式模型。 DirectQuery、資料分割、資料列層級安全性、雙向關聯性和翻譯全都支援。 若要進一步了解，請參閱[Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/)。

**SQL Server Analysis Services** -支援表格式模型在所有相容性層級、 多維度模型、 資料採礦和 Power Pivot for SharePoint。

## <a name="documentation-by-area"></a>依區域列出的文件

一般情況下， [Azure Analysis Services 文件](https://docs.microsoft.com/azure/analysis-services/)隨附 Azure 文件。 如果您想要在雲端中有您的表格式模型，最好是從該文開始。 此發行項與本節中的文件主要是用於 SQL Server Analysis Services。 不過，至少針對表格式模型，如何建立及部署表格式模型專案是不變，不論您使用的平台。 請檢查下列各節，若要深入了解：

- [比較表格式和多維度解決方案](../analysis-services/comparing-tabular-and-multidimensional-solutions-ssas.md)
- [安裝 SQL Server Analysis Services](../analysis-services/instances/install-windows/install-analysis-services.md)
- [表格式模型](../analysis-services/tabular-models/tabular-models-ssas.md)
- [多維度模型](../analysis-services/multidimensional-models/multidimensional-models-ssas.md)
- [資料採礦](../analysis-services/data-mining/data-mining-ssas.md)
- [Power Pivot for SharePoint](../analysis-services/power-pivot-sharepoint/power-pivot-for-sharepoint-ssas.md)
- [教學課程](../analysis-services/analysis-services-tutorials-ssas.md)
- [伺服器管理](../analysis-services/instances/analysis-services-instance-management.md)
- [開發人員文件](analysis-services-developer-documentation.md)
- [技術參考](https://docs.microsoft.com/bi-reference/)

#### <a name="see-also"></a>另請參閱

[Azure Analysis Services 文件](https://docs.microsoft.com/azure/analysis-services/)
[SQL Server 文件](../sql-server/sql-server-technical-documentation.md)
