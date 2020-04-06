---
title: SQL Server 2019 版本資訊 | Microsoft Docs
description: 尋找 SQL Server 2019 (15.x) 限制、已知問題、協助資源，以及其他版本資訊的相關資訊。
ms.date: 11/04/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: release-landing
ms.topic: article
ms.assetid: 13942af8-5a40-4cef-80f5-918386767a47
author: MikeRayMSFT
ms.author: mikeray
monikerRange: = sql-server-ver15 || = sqlallproducts-allversions
ms.openlocfilehash: 67e08192643337ec37ef0be3bd603599d25a769d
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/04/2020
ms.locfileid: "80665416"
---
# <a name="sql-server-2019-release-notes"></a>[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] 版本資訊
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

此文章說明 [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] 的限制與已知問題。 如需相關資訊，請參閱：

> [[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] 的新功能](../sql-server/what-s-new-in-sql-server-ver15.md)

## [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] 是 [!INCLUDE[SQL Server 2019](../includes/ssnoversion-md.md)] 最新的公開版本。

授權的完整詳細資料位於安裝媒體上 `License Terms` 資料夾中。

## <a name="documentation"></a>文件

- **問題和對客戶的影響**：可以依版本篩選 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 文件。 使用每個文件頁面左上方控制項來篩選您的需求。

## <a name="build-number"></a>組建編號

SQL Server 2019 的 RTM 組建編號是 `15.0.2000.5`。

[!INCLUDE [sql-server-servicing-updates-version-15](../includes/sql-server-servicing-updates-version-15.md)]

## <a name="sql-server-installation-may-fail-if-ssms-18x-is-installed"></a>如果已安裝 SSMS 18.x，SQL Server 安裝可能會失敗

- **問題與對客戶的影響**：當依序進行下列安裝時，[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] 安裝失敗：
  1. 在伺服器上安裝 SQL Server Management Studio (SSMS) 18.0、18.1、18.2 或 18.3 版。
  1. 嘗試從抽取式媒體進行 [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] 安裝。 例如，安裝媒體是 DVD。

- **因應措施**：
  1. 解除安裝比 SSMS 18.3.1 舊的任何版本。
  1. 安裝比 SSMS (18.3.1 或更新版本) 新的任何版本。 如需最新版本，請參閱[下載 SSMS](../ssms/download-sql-server-management-studio-ssms.md)。
  1. 以正常方式安裝 [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)]。

- **適用於**：[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)]

## <a name="utf-8-collations"></a>UTF-8 定序

- **問題和對客戶的影響**︰啟用 UTF-8 的定序不能與下列功能搭配使用：
  - [記憶體內部 OLTP 資料表](../relational-databases/in-memory-oltp/introduction-to-memory-optimized-tables.md)
  - [具有安全記憶體保護區的 Always Encrypted](../relational-databases/security/encryption/always-encrypted-enclaves.md) (不使用安全記憶體保護區時，[Always Encrypted](../relational-databases/security/encryption/always-encrypted-database-engine.md) 可以使用 UTF-8)

  > [!WARNING]
  > 建立資料庫的 [bacpac](../relational-databases/data-tier-applications/data-tier-applications.md#bacpac)，其中包含資料表資料行定義為使用超過 4000 個位元組的 [CHAR 或 VARCHAR](../t-sql/data-types/char-and-varchar-transact-sql.md) 將會失敗。
  
  > [!NOTE]
  > 在 Azure Data Studio 或 SQL Server Data Tools (SSDT) 中，目前沒有可選擇啟用 UTF-8 之定序的 UI 支援。 最新 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] (SSMS) 18 版支援在 UI 中選擇啟用 UTF-8 的定序。

- **適用於**：[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] RTM

## <a name="master-data-service-notification-email-contains-broken-link"></a>Master Data Service 通知電子郵件包含中斷的連結

- **問題和對客戶的影響**︰來自 Master Data Services (MDS) 的通知電子郵件包含中斷的連結。 此連結會巡覽至傳回錯誤的頁面，如下列訊息所示：

   `The view 'Index' or its master was not found or no view engine supports the searched locations.`

- **因應措施**：開啟 MDS 入口網站，並手動移至資源。

- **適用於**：[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] RTM

## <a name="see-also"></a>另請參閱

- [安裝 SQL Server 的硬體與軟體需求](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server-ver15.md)

## <a name="machine-learning-services"></a>機器學習服務

如需 SQL Server Microsoft 機器學習服務中的問題，請參閱 [SQL Server Microsoft 機器學習服務機器學習服務中的已知問題](../machine-learning/known-issues-for-sql-server-machine-learning-services.md)。

[!INCLUDE[get-help-options-msft-only](../includes/paragraph-content/get-help-options.md)]
