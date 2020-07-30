---
title: 輪替 | Microsoft Docs
ms.custom: ''
ms.date: 10/31/2019
ms.prod: sql
ms.reviewer: vanto
ms.prod_service: database-engine, sql-database
ms.technology: security
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 5420d49b6e5d165168610d002424e3a3b9499748
ms.sourcegitcommit: 620a868e623134ad6ced6728ce9d03d7d0038fe0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/29/2020
ms.locfileid: "87411054"
---
# <a name="rotate-enclave-enabled-keys"></a>輪替已啟用記憶體保護區的金鑰
[!INCLUDE [sqlserver2019-windows-only](../../../includes/applies-to-version/sqlserver2019-windows-only.md)]

在 Always Encrypted 中，金鑰輪替是將現有資料行主要金鑰或資料行加密金鑰更換成新金鑰的程序。 本文描述當初始金鑰和/或目標 (新) 金鑰是已啟用記憶體保護區的金鑰時，[具有安全記憶體保護區的 Always Encrypted](always-encrypted-enclaves.md) 特定金鑰輪替的使用案例和考量。 如需管理 Always Encrypted 金鑰的一般指導方針和程序，請參閱 [Always Encrypted 的金鑰管理概觀](overview-of-key-management-for-always-encrypted.md)。 

您可能基於安全性或合規性理由，而需要輪替金鑰。 例如，如果金鑰已遭洩漏，或您的組織原則要求您定期更換金鑰。 此外，具有安全記憶體保護區的 Always Encrypted 金鑰輪替可讓您為加密資料行啟用或停用伺服器端安全記憶體保護區的功能。
- 當將未啟用記憶體保護區的金鑰更換成已啟用記憶體保護區的金鑰時，您會解除鎖定安全記憶體保護區的功能，在以該金鑰所保護的一或多個資料行上進行查詢。 請參閱[為現有加密資料行啟用具有安全記憶體保護區的 Always Encrypted](always-encrypted-enclaves-enable-for-encrypted-columns.md)。
 - 當您將已啟用記憶體保護區的金鑰更換成未啟用記憶體保護區的金鑰時，會停用安全記憶體保護區的功能，在以該金鑰所保護的一或多個資料行上進行查詢。

如果您只是基於安全性/合規性理由輪替金鑰，而不是為了啟用或停用資料行的記憶體保護區計算，請確定目標金鑰與來源金鑰具有相同的記憶體保護區相關設定。 例如，如果來源金鑰已啟用記憶體保護區，則目標金鑰也應該啟用記憶體保護區。

以下高階步驟包含詳細文章的連結 (取決於您的輪替案例)：

1. 佈建新的金鑰 (資料行主要金鑰或資料行加密金鑰)。
    - 若要佈建已啟用記憶體保護區的新金鑰，請參閱[佈建已啟用記憶體保護區的金鑰](always-encrypted-enclaves-provision-keys.md)。
    - 若要佈建未啟用記憶體保護區的金鑰，請參閱[使用 SQL Server Management Studio 佈建 Always Encrypted 金鑰](configure-always-encrypted-keys-using-ssms.md)和[使用 PowerShell 佈建 Always Encrypted 金鑰](configure-always-encrypted-keys-using-powershell.md)。
2. 將現有金鑰更換成新的金鑰。
    - 如果您要輪替資料行加密金鑰，且來源金鑰和目標金鑰都已啟用記憶體保護區，您可以就地執行輪替 (這會涉及重新加密資料)。 請參閱[使用具有安全記憶體保護區的 Always Encrypted 就地設定資料行加密](always-encrypted-enclaves-configure-encryption.md)。
    - 如需輪替金鑰的詳細步驟，請參閱[使用 SQL Server Management Studio 輪替 Always Encrypted 金鑰](rotate-always-encrypted-keys-using-ssms.md)和[使用 PowerShell 輪替 Always Encrypted 金鑰](rotate-always-encrypted-keys-using-powershell.md)。

    
## <a name="next-steps"></a>後續步驟
- [使用具有安全記憶體保護區的 Always Encrypted 查詢資料行](always-encrypted-enclaves-query-columns.md)
- [使用具有安全記憶體保護區的 Always Encrypted 就地設定資料行加密](always-encrypted-enclaves-configure-encryption.md)
- [為現有加密資料行啟用具有安全記憶體保護區的 Always Encrypted](always-encrypted-enclaves-enable-for-encrypted-columns.md)
- [使用具有安全記憶體保護區的 Always Encrypted 開發應用程式](always-encrypted-enclaves-client-development.md)  

## <a name="see-also"></a>另請參閱  
- [為具有安全記憶體保護區的 Always Encrypted 管理金鑰](always-encrypted-enclaves-manage-keys.md)

