---
description: 使用具有安全記憶體保護區的 Always Encrypted 與 SSMS 查詢資料行
title: 使用具有安全記憶體保護區的 Always Encrypted 與 SSMS 查詢資料行 | Microsoft Docs
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
ms.openlocfilehash: cf739bc33c505de3edac3869f4e5b095b651ed8a
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97477569"
---
# <a name="query-columns-using-always-encrypted-with-secure-enclaves-with-ssms"></a>使用具有安全記憶體保護區的 Always Encrypted 與 SSMS 查詢資料行
[!INCLUDE [sqlserver2019-windows-only](../../../includes/applies-to-version/sqlserver2019-windows-only.md)]

本文描述如何使用 SQL Server Management Studio 來發出查詢，為[具有安全記憶體保護區的 Always Encrypted](always-encrypted-enclaves.md) 使用伺服器端安全記憶體保護區，包括：
- 觸發就地密碼編譯作業的查詢。
- 觸發豐富計算的查詢，包括在資料行 (使用已啟用記憶體保護區的金鑰加密) 上進行範圍比較或模式比對作業。
- 使用隨機化加密和已啟用記憶體保護區的金鑰，在加密資料行上建立或更新索引的查詢。  

若要使用 SSMS 以利用安全記憶體保護區在加密資料行上執行查詢，請遵循[使用 Always Encrypted 與 SQL Server Management Studio 查詢資料行](always-encrypted-query-columns-ssms.md)中的指示。 以下是您應該注意的一些記憶體保護區特定事項：

- 您需要 SSMS 18.3 版或更高版本。
- 請確定您是在查詢視窗中執行查詢，而該查詢視窗會透過已啟用 Always Encrypted 和記憶體保護區計算的連線來利用安全記憶體保護區。 如需詳細指示，請參閱[教學課程：使用 SSMS，開始使用具有安全記憶體保護區的 Always Encrypted](../tutorial-getting-started-with-always-encrypted-enclaves.md) 和[針對資料庫連接啟用和停用 Always Encrypted](always-encrypted-query-columns-ssms.md#en-dis)。

## <a name="next-steps"></a>後續步驟
- [使用具有安全記憶體保護區的 Always Encrypted 開發應用程式](always-encrypted-enclaves-client-development.md)

## <a name="see-also"></a>另請參閱  
- [教學課程：使用 SSMS，開始使用具有安全記憶體保護區的 Always Encrypted](../tutorial-getting-started-with-always-encrypted-enclaves.md)
- [使用 Transact-SQL 就地設定資料行加密](always-encrypted-enclaves-configure-encryption-tsql.md)
- [使用具有安全記憶體保護區的 Always Encrypted 在資料行上建立及使用索引](always-encrypted-enclaves-create-use-indexes.md)

