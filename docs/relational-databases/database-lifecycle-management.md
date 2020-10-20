---
title: 資料庫生命週期管理 (DLM) | Microsoft 文件
description: 了解如何使用 SQL Server 中的資料庫生命週期管理，針對效能、保護、可用性及成本來管理資料庫和資料資產。
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- Data sync
- SQL Database
- Azure Training Kit
- Database development
- Database backup
- Database connection management
- Database community
- Backup and restore
- Database import and export
- SQL Data Sync
- Azure Service Dashboard
- SQL Server Management Studio
- Database management
- Database export
- SQL Server Data Tools
- SSMS
- SSDT
- Database migration
- Database connectivity
ms.assetid: 91da13a4-0eea-4e88-b608-dada881ff5f2
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 604fbce3aebe8e6e902e2dc9292a24779471c86e
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/19/2020
ms.locfileid: "92196206"
---
# <a name="database-lifecycle-management"></a>資料庫生命週期管理
[!INCLUDE [SQL Server Azure SQL Database](../includes/applies-to-version/sql-asdb.md)]
  資料庫生命週期管理 (DLM) 是一種管理資料庫和資料資產的原則式方法。 DLM 不是產品而是一套針對資料庫應用程式管理資料庫結構描述、資料和中繼資料的完整方法。 周全且主動的 DLM 方法可讓組織根據適當的效能、保護、可用性和成本層級管理資料資源。  
  
 DLM 一開始會探討專案設計與意圖，接著探討資料庫開發、測試、建置、部署、維護、監視和備份活動，最後再探討資料封存。 本主題將提供 DLM 各階段的概觀：從資料庫開發開始，然後依序進行建置、部署和監視動作。 同時也包含資料管理活動，以及資料可攜性作業，例如匯入/匯出、備份、移轉和同步。  
  
 若要閱讀完整主題，請參閱 [Database Lifecycle Management (DLM)](/previous-versions/sql/sql-server-guides/jj907294(v=sql.110))(資料庫生命週期管理 (DLM))。  
  
## <a name="see-also"></a>另請參閱  
 [Azure 首頁](https://www.windowsazure.com/)   
 [Azure 開發人員中心](https://www.windowsazure.com/develop/overview/)   
 [Azure 管理中心](https://www.windowsazure.com/manage/overview/)   
 [Azure 團隊部落格](https://www.windowsazure.com/community/blog/)   
 [Azure 支援選項](https://www.windowsazure.com/support/contact/)  
  
