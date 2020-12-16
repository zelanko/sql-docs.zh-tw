---
description: 使用具有安全記憶體保護區的 Always Encrypted 查詢資料行
title: 使用具有安全記憶體保護區的 Always Encrypted 查詢資料行 | Microsoft Docs
ms.custom: ''
ms.date: 10/31/2019
ms.reviewer: vanto
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: security
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15'
ms.openlocfilehash: 517e2a0beb7364507d585d9cd729069048cf1c82
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97477559"
---
# <a name="query-columns-using-always-encrypted-with-secure-enclaves"></a>使用具有安全記憶體保護區的 Always Encrypted 查詢資料行
[!INCLUDE [sqlserver2019-windows-only](../../../includes/applies-to-version/sqlserver2019-windows-only.md)]

本文會記錄針對[具有安全記憶體保護區的 Always Encrypted](always-encrypted-enclaves.md) 使用伺服器端安全記憶體保護區，在加密資料行上執行查詢的一般考量。 

下列查詢類型牽涉到使用安全記憶體保護區：
- 使用已啟用記憶體保護區之金鑰來觸發就地密碼編譯作業的查詢 - 請參閱[使用 Transact-SQL 就地設定資料行加密](always-encrypted-enclaves-configure-encryption-tsql.md)。
- 豐富查詢 - 在資料行 (使用隨機化加密和已啟用記憶體保護區的金鑰加密) 上進行範圍比較或模式比對作業。
- 使用隨機化加密和已啟用記憶體保護區的金鑰，在加密資料行上建立或更新索引的查詢。 如需詳細資訊，請參閱[使用具有安全記憶體保護區的 Always Encrypted 在資料行上建立及使用索引](always-encrypted-enclaves-create-use-indexes.md)。

> [!NOTE]
> 只有使用隨機化加密且已啟用記憶體保護區的資料行 (使用已啟用記憶體保護區的資料行加密金鑰所加密資料行) 才支援豐富查詢和索引。 確定性加密不支援豐富的查詢或索引。

> [!NOTE]
> 在加密字元字串資料行上進行的豐富查詢，需要資料行使用具有 binary2 排序次序 (BIN2 定序) 的定序。 


## <a name="next-steps"></a>後續步驟
- [使用具有安全記憶體保護區的 Always Encrypted 與 SSMS 查詢資料行](always-encrypted-enclaves-query-columns-ssms.md)

## <a name="see-also"></a>另請參閱
- [教學課程：使用 SSMS，開始使用具有安全記憶體保護區的 Always Encrypted](../tutorial-getting-started-with-always-encrypted-enclaves.md)

