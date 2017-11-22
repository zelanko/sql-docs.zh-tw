---
title: "Microsoft SQL 和 GDPR 需求 | Microsoft Docs"
ms.custom: 
ms.date: 05/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: security
ms.reviewer: 
ms.suite: sql
ms.technology: sql-security
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: "2"
author: barbkess
ms.author: ronitr
manager: craigg
ms.openlocfilehash: a98e19f8bea8b8a1d1679cee6bb7a86215c48450
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="guide-to-enhancing-privacy-and-addressing-gdpr-requirements-with-the-microsoft-sql-platform"></a>使用 Microsoft SQL 平台加強隱私權和解決 GDPR 需求的指南
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

## <a name="summary"></a>摘要
歐洲的隱私權法將在 2018 年 5 月25 日生效，在隱私權權限、安全性與合規性方面設定了新的全球標準。 一般資料保護規範或 GDPR，本質上是關於保護及賦予個人隱私權權限，並在尊重個人選擇的情況下，制定嚴格的全球隱私權需求來控管個人資料的管理及保護方式。 

受限於 GDPR 的 Microsoft SQL 客戶，不論是管理雲端式或內部部署資料庫還是管理這兩者，都必須確保其資料庫系統中的合格資料已根據 GDPR 準則適當地處理及保護。 這表示許多客戶需要檢閱或修改其資料庫管理和資料處理程序，尤其著重在 GDPR 所規定的資料處理安全性。

以 Microsoft SQL 為基礎的技術提供許多內建的安全性功能，可協助降低資料風險，並改善資料庫層級與更高層級的資料保護和可管理性。 這份文件可檢查這些功能，並分享一些使用 Microsoft SQL 來達到 GDPR 資料隱私權目標的 Microsoft 獨有方法。
   
  
**作者：**Ronit Reger

**技術校閱：**Conor Cunningham；Joachim Hammer；Shai Kariv；Julie Koesmarno；Alice Kupcik；Ron Matchoro；Gilad Mittelman；Dan Rediske；Tomer Weisberg 
  
**發佈日期：**2017 年 5 月  
  
**適用於：**SQL Server (所有版本)、Azure SQL Database、Azure SQL 資料倉儲、Analytics Platform System 
  
若要檢閱文件，請下載 [使用 Microsoft SQL 平台加強隱私權和解決 GDPR 需求的指南](http://download.microsoft.com/download/4/9/4/4948194B-A613-49ED-90A5-5144313549AB/microsoft-sql-and-the-gdpr.pdf)文件。   
