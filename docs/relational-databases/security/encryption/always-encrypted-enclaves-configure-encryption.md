---
title: 使用具有安全記憶體保護區的 Always Encrypted 就地設定資料行加密 | Microsoft Docs
ms.custom: ''
ms.date: 10/10/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: d887e428773e6901544422edcb6960e6e9ae0580
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/05/2019
ms.locfileid: "73595513"
---
# <a name="configure-column-encryption-in-place-using-always-encrypted-with-secure-enclaves"></a>使用具有安全記憶體保護區的 Always Encrypted 就地設定資料行加密 
[!INCLUDE [tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly](../../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly.md)]

[具有安全記憶體保護區的 Always Encrypted](always-encrypted-enclaves.md) 支援在資料庫資料行上就地進行密碼編譯作業 (即在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中的安全記憶體保護區內部進行)。 就地加密讓您無須針對這類作業將資料移出資料庫，使密碼編譯作業更快且更加可靠。 

> [!NOTE]
> 雖然就地加密具有效能優點，但在大型資料表上進行密碼編譯作業可能需要很長時間並取用大量資源，且可能因此影響或降低應用程式的效能和可用性。

就地加密可讓您使用 [ALTER TABLE ALTER COLUMN (Transact-SQL)](../../../t-sql/statements/alter-table-transact-sql.md) 陳述式觸發密碼編譯作業，這在沒有記憶體保護區的情況下是不可能的。

## <a name="prerequisites"></a>Prerequisites
所支援密碼編譯作業及針對作業所需要使用資料行加密金鑰的需求如下：
- 加密純文字資料行。 用來加密資料行的資料行加密金鑰必須已啟用記憶體保護區。
- 使用新加密類型和/或新的資料行加密金鑰重新加密已加密的資料行。 目前的資料行加密金鑰和新資料行加密金鑰 (若與目前的金鑰不同) 都必須已啟用記憶體保護區。
- 解密已加密的資料行 - 保護資料行的資料行加密金鑰必須已啟用記憶體保護區。

請參閱[針對具有安全記憶體保護區的 Always Encrypted 管理金鑰](always-encrypted-enclaves-manage-keys.md)，以取得如何確認資料行加密金鑰已啟用記憶體保護區的資訊。

就地加密也需要具備正確初始化安全記憶體保護區的 SQL Server 執行個體。 請參閱[設定 Always Encrypted 伺服器設定選項的記憶體保護區類型](../../../database-engine/configure-windows/configure-column-encryption-enclave-type.md)。

觸發密碼編譯作業之使用者或應用程式必須具備對包含受影響資料行資料表進行結構描述變更的權限，以及存取作業中所涉及資料行主要金鑰和資料庫中相關金鑰中繼資料的權限。

您只能從 SQL Server Management Studio 或自訂應用程式，使用 [ALTER TABLE ALTER COLUMN (Transact-SQL)](../../../t-sql/statements/alter-table-transact-sql.md) 來觸發就地加密。 請參閱[使用 Transact-SQL 就地設定資料行加密](always-encrypted-enclaves-configure-encryption-tsql.md)。

> [!NOTE]
> 目前，[Always Encrypted 精靈](always-encrypted-wizard.md)和 [Set-SqlColumnEncryption](https://docs.microsoft.com/powershell/module/sqlserver/set-sqlcolumnencryption) Cmdlet 不支援就地加密，且即使設定滿足上述需求，也一律會下載資料以進行密碼編譯作業。 

## <a name="next-steps"></a>Next Steps
- [使用 Transact-SQL 就地設定資料行加密](always-encrypted-enclaves-configure-encryption-tsql.md)
- [使用具有安全記憶體保護區的 Always Encrypted 在資料行上建立及使用索引](always-encrypted-enclaves-create-use-indexes.md)
- [使用具有安全記憶體保護區的 Always Encrypted 開發應用程式](always-encrypted-enclaves-client-development.md)
