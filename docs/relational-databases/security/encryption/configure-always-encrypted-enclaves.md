---
title: 設定和使用具有安全記憶體保護區的 Always Encrypted | Microsoft Docs
description: 了解如何在 SQL Server 中搭配安全記憶體保護區設定及使用 Always Encrypted，以在敏感性資料上啟用更豐富的功能。
ms.custom: ''
ms.date: 10/18/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: d73d337e750e287066531017710b733c92a312ff
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85627024"
---
# <a name="configure-and-use-always-encrypted-with-secure-enclaves"></a>設定和使用具有安全記憶體保護區的 Always Encrypted 

[!INCLUDE[SQL Server 2019](../../../includes/applies-to-version/sqlserver2019.md)]

[具有安全記憶體保護區的 Always Encrypted](always-encrypted-enclaves.md) 會擴充現有 [Always Encrypted](always-encrypted-database-engine.md) 功能，以啟用更豐富的敏感性資料功能，同時保持資料的機密性。 本文列出設定和使用功能的一般工作。

如需示範如何透過安全記憶體保護區快速開始使用 Always Encrypted 的教學課程，請參閱[教學課程：使用 SSMS，開始使用具有安全記憶體保護區的 Always Encrypted](../tutorial-getting-started-with-always-encrypted-enclaves.md)。

## <a name="set-up-your-environment-to-support-enclaves-and-attestation"></a>設定您的環境以支援記憶體保護區和證明
如需詳細資料，請參閱下文：
- [規劃主機守護者服務證明](./always-encrypted-enclaves-host-guardian-service-plan.md)
- [針對 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 部署主機守護者服務](./always-encrypted-enclaves-host-guardian-service-deploy.md)
- [向主機守護者服務註冊您的電腦](./always-encrypted-enclaves-host-guardian-service-register.md)

## <a name="manage-keys-for-always-encrypted-with-secure-enclaves"></a>針對具有安全記憶體保護區的 Always Encrypted 管理金鑰
如需詳細資料，請參閱下文：
- [針對具有安全記憶體保護區的 Always Encrypted 管理金鑰 - 概觀](always-encrypted-enclaves-manage-keys.md)
- [佈建已啟用記憶體保護區的金鑰](always-encrypted-enclaves-provision-keys.md)
- [輪替已啟用記憶體保護區的金鑰](always-encrypted-enclaves-rotate-keys.md)

## <a name="configure-columns-with-always-encrypted-with-secure-enclaves"></a>使用具有安全記憶體保護區的 Always Encrypted 設定資料行
如需詳細資料，請參閱下文：
- [使用具有安全記憶體保護區的 Always Encrypted 就地設定資料行加密 - 概觀](always-encrypted-enclaves-configure-encryption.md)
- [使用 Transact-SQL 就地設定資料行加密](always-encrypted-enclaves-configure-encryption-tsql.md)
- [為現有加密資料行啟用具有安全記憶體保護區的 Always Encrypted](always-encrypted-enclaves-enable-for-encrypted-columns.md)

> [!NOTE]
> 如需有關如何設定測試環境並在 SSMS 中嘗試具有安全記憶體保護區之 Always Encrypted 功能的逐步教學課程，請參閱[教學課程：使用 SSMS，開始使用具有安全記憶體保護區的 Always Encrypted](../tutorial-getting-started-with-always-encrypted-enclaves.md)。

## <a name="query-columns-using-always-encrypted-with-secure-enclaves"></a>使用具有安全記憶體保護區的 Always Encrypted 查詢資料行
如需詳細資料，請參閱下文：
- [使用具有安全記憶體保護區的 Always Encrypted 查詢資料行 - 概觀](always-encrypted-enclaves-query-columns.md)
- [使用具有安全記憶體保護區的 Always Encrypted 與 SSMS 查詢資料行](always-encrypted-enclaves-query-columns-ssms.md)

## <a name="create-and-use-indexes-on-enclave-enabled-columns"></a>在已啟用記憶體保護區的資料行上建立和使用索引
如需詳細資料，請參閱下文：
- [使用具有安全記憶體保護區的 Always Encrypted 在資料行上建立及使用索引](always-encrypted-enclaves-create-use-indexes.md)

## <a name="develop-applications-using-always-encrypted-with-secure-enclaves"></a>使用具有安全記憶體保護區的 Always Encrypted 開發應用程式
如需詳細資料，請參閱下文：
- [使用具有安全記憶體保護區的 Always Encrypted 開發應用程式](always-encrypted-enclaves-client-development.md)
