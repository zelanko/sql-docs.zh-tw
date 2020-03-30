---
title: 使用 Always Encrypted 備份和還原資料庫 | Microsoft Docs
ms.custom: ''
ms.date: 10/30/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
ms.assetid: 29816a41-f105-4414-8be1-070675d62e84
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 9176052b413293d25acd7696701e4f118adba03f
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "73595723"
---
# <a name="backup-and-restore-databases-using-always-encrypted"></a>使用 Always Encrypted 備份和還原資料庫 
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

本文描述如何備份和還原包含以 [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md) 所保護資料行的資料庫。

當您備份資料庫時，所產生備份檔案會包含儲存在加密資料行中的加密資料，以及 Always Encrypted 金鑰的所有中繼資料。

當您還原資料庫時，所有加密資料和 Always Encrypted 金鑰的所有中繼資料都會還原。 

如果您將資料庫還原到不同伺服器或不同名稱，則不需要執行任何特殊動作來讓應用程式查詢目標資料庫中的加密資料，因為這兩個資料庫中的金鑰都相同。

如需如何備份和還原資料庫的詳細資訊，請參閱：
- [備份概觀 (SQL Server)](../../backup-restore/backup-overview-sql-server.md)
- [將資料庫還原到受控執行個體](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-get-started-restore)

## <a name="next-steps"></a>後續步驟
- [使用 Always Encrypted 與 SQL Server Management Studio 查詢資料行](always-encrypted-query-columns-ssms.md)
- [使用具有安全記憶體保護區的 Always Encrypted 開發應用程式](always-encrypted-enclaves-client-development.md) 

## <a name="see-also"></a>另請參閱
- [一律加密](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [使用 Always Encrypted 匯出和匯入資料庫](always-encrypted-migrate-using-bacpac.md)
- [使用 Always Encrypted 與 SQL Server [匯入及匯出精靈]，將資料移轉進或移轉出資料行](always-encrypted-migrate-using-import-export-wizard.md)
- [使用 Always Encrypted 將加密資料大量載入至資料行](migrate-sensitive-data-protected-by-always-encrypted.md)
