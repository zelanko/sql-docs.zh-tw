---
title: 使用具有安全記憶體保護區的 Always Encrypted 開發應用程式 | Microsoft Docs
ms.custom: ''
ms.date: 10/15/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
dev_langs:
- CSharp
ms.assetid: 9595eb66-284c-4474-828f-8961a05ce989
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7ec032a9a6bd6d02372d77d8844d5e4938fbe945
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "74492010"
---
# <a name="develop-applications-using-always-encrypted-with-secure-enclaves"></a>使用具有安全記憶體保護區的 Always Encrypted 開發應用程式
[!INCLUDE [tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly](../../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly.md)]

[具有安全記憶體保護區的 Always Encrypted](always-encrypted-enclaves.md) 會延伸 [Always Encrypted](always-encrypted-database-engine.md)，讓您在已加密敏感性資料庫資料行上使用更豐富的應用程式查詢功能。 其利用安全記憶體保護區技術，讓 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 中的查詢執行程式將加密資料行上計算委派給 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 處理序內的安全記憶體保護區。

## <a name="client-driver-for-always-encrypted-with-secure-enclaves"></a>具有安全記憶體保護區 Always Encrypted 的用戶端驅動程式

若要使用具有安全記憶體保護區的 Always Encrypted 開發應用程式，您需要支援安全記憶體保護區的 SQL 用戶端驅動程式版本。 用戶端驅動程式扮演下列關鍵角色：
- 在將使用安全記憶體保護區的查詢提交給 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)]執行前，驅動程式會起始記憶體保護區證明，驗證安全記憶體保護區為可信任，並可以安全地使用該記憶體保護區來處理敏感性資料。 如需證明的詳細資訊，請參閱[安全記憶體保護區證明](always-encrypted-enclaves.md#secure-enclave-attestation)。
- 證明成功後，用戶端驅動程式會透過交涉共用祕密，與記憶體保護區建立安全工作階段。
- 驅動程式會使用共用祕密來加密記憶體保護區處理查詢時將需要的資料行加密金鑰，並將金鑰傳送到 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)]，其會將金鑰轉寄到解密金鑰的安全記憶體保護區。 
- 最後，驅動程式會提交查詢以執行，在安全記憶體保護區內部觸發計算。

若要使用安全記憶體保護區的功能，您需要設定應用程式和用戶端驅動程式，在連線到資料庫時啟用記憶體保護區計算，並指定指向您記憶體保護區證明服務的證明服務端點 (記憶體保護區證明 URL)。 詳細資料取決於您正在使用的驅動程式和證明服務/通訊協定。

## <a name="next-steps"></a>後續步驟

下列用戶端驅動程式支援具有安全記憶體保護區的 Always Encrypted：
- .NET Framework 4.7.2 或更新版本中的 .NET Framework Data Provider for SQL Server。 
    - 如需詳細資訊，請參閱[搭配 .NET Framework Data Provider for SQL Server 使用 Always Encrypted](../../../relational-databases/security/encryption/develop-using-always-encrypted-with-net-framework-data-provider.md)。
    - 如需逐步教學課程，請參閱[教學課程：使用具有安全記憶體保護區的 Always Encrypted 開發 .NET Framework 應用程式](../tutorial-always-encrypted-enclaves-develop-net-framework-apps.md)
- .NET Framework 4.6 或更新版本，以及 .NET Core 2.1 或更新版本中的 Microsoft .NET Data Provider for SQL Server。 
    - 如需詳細資訊，請參閱[搭配 Microsoft .NET Data Provider for SQL Server 使用 Always Encrypted](../../../connect/ado-net/sql/sqlclient-support-always-encrypted.md)。
    - 如需逐步教學課程，請參閱[教學課程：使用具有安全記憶體保護區的 Always Encrypted 開發 .NET 應用程式](../../../connect/ado-net/sql/tutorial-always-encrypted-enclaves-develop-net-apps.md)
- Microsoft ODBC Driver for SQL Server 版本 17.4 或更新版本。 
    - 如需詳細資訊，請參閱[搭配 ODBC 驅動程式使用 Always Encrypted](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md)。 
    - 如需如何為使用 ODBC 之資料庫連接啟用記憶體保護區計算的資訊，請參閱[啟用具有安全記憶體保護區的 Always Encrypted](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md#enabling-always-encrypted-with-secure-enclaves) 一節。
