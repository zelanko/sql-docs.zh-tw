---
description: 針對具有安全記憶體保護區的 Always Encrypted 管理金鑰
title: 為具有安全記憶體保護區的 Always Encrypted 管理金鑰 | Microsoft Docs
ms.custom: ''
ms.date: 10/30/2019
ms.reviewer: vanto
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: security
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15'
ms.openlocfilehash: 0c1f00a5b1e69bdb8f51f848210e8e90b0ae6a4b
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97477629"
---
# <a name="manage-keys-for-always-encrypted-with-secure-enclaves"></a>針對具有安全記憶體保護區的 Always Encrypted 管理金鑰
[!INCLUDE [sqlserver2019-windows-only](../../../includes/applies-to-version/sqlserver2019-windows-only.md)]

[具有安全記憶體保護區的 Always Encrypted](always-encrypted-enclaves.md) 會藉由引進已啟用記憶體保護區的金鑰，來擴充 [Always Encrypted](always-encrypted-database-engine.md) 的金鑰管理： 

- **已啟用記憶體保護區的資料行主要金鑰** - 使用 `ENCLAVE_COMPUTATIONS` 屬性 (於資料庫內部的資料行主要金鑰中繼資料物件中指定) 建立的資料行主要金鑰。 
- **已啟用記憶體保護區的資料行加密金鑰** - 以已啟用記憶體保護區的資料行主要金鑰進行加密的資料行加密金鑰。 只有已啟用記憶體保護區的資料行加密金鑰才能用於伺服器端安全記憶體保護區內計算。 

[管理 Always Encrypted 金鑰](overview-of-key-management-for-always-encrypted.md)的一般方針和處理序，適用於管理已啟用記憶體保護區的金鑰。 

## <a name="managing-keys"></a>管理金鑰

下列文章討論以下特定層面：管理已啟用記憶體保護區的金鑰。

- [佈建已啟用記憶體保護區的金鑰](always-encrypted-enclaves-provision-keys.md)
- [輪替已啟用記憶體保護區的金鑰](always-encrypted-enclaves-rotate-keys.md)

## <a name="next-steps"></a>後續步驟
- [佈建已啟用記憶體保護區的金鑰](always-encrypted-enclaves-provision-keys.md)

## <a name="see-also"></a>另請參閱  
- [Always Encrypted 的金鑰管理概觀](overview-of-key-management-for-always-encrypted.md)
- [CREATE COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/create-column-master-key-transact-sql.md)
