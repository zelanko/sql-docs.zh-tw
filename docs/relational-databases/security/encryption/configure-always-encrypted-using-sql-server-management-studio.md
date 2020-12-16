---
title: 使用 SSMS 設定永遠加密
description: 描述搭配 SQL Server Management Studio (SSMS) 來設定及管理 Always Encrypted 資料庫的工作。
ms.custom: seo-lt-2019
ms.date: 10/31/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Always Encrypted, configure with SSMS
ms.assetid: 29816a41-f105-4414-8be1-070675d62e84
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d3d018e1cd1230e50702192ebc675fd2ed1b155f
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97459990"
---
# <a name="configure-always-encrypted-using-sql-server-management-studio"></a>使用 SQL Server Management Studio 設定永遠加密
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]

本文所說明的工作是有關設定永遠加密以及管理搭配使用永遠加密與 [SQL Server Management Studio (SSMS)](../../../ssms/download-sql-server-management-studio-ssms.md)的資料庫。

## <a name="security-considerations-when-using-ssms-to-configure-always-encrypted"></a>使用 SSMS 設定 Always Encrypted 時的安全性考量

當您使用 SSMS 設定永遠加密時，SSMS 會同時處理永遠加密金鑰和敏感性資料，因此金鑰和資料會以純文字形式出現在 SSMS 處理序內。 因此，請務必在安全的電腦上執行 SSMS。 如果您的資料庫裝載在 SQL Server 上，請確定在與裝載 SQL Server 執行個體不同的電腦上執行 SSMS。 因為永遠加密的主要目標是為了確保已加密的敏感性資料安全無虞，即使資料庫系統遭到入侵亦然，所以在 SQL Server 電腦上執行處理金鑰或敏感性資料的 PowerShell 指令碼，可能會降低或損害此功能的優點。 如需其他建議，請參閱 [金鑰管理的安全性考量](overview-of-key-management-for-always-encrypted.md#security-considerations-for-key-management)。

SSMS 不支援下列兩者之間的角色隔離：管理資料庫的人員 (DBA) 與管理密碼編譯密碼且有權存取純文字資料的人員 (安全性系統管理員和/或應用程式系統管理員)。 如果您的組織強制執行角色隔離，則應該使用 PowerShell 設定永遠加密。 如需詳細資訊，請參閱 [Always Encrypted 的金鑰管理概觀](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)和[使用 PowerShell 設定 Always Encrypted](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md)。 

## <a name="always-encrypted-tasks-using-ssms"></a>使用 SSMS 的 Always Encrypted 工作

- [使用 SQL Server Management Studio 佈建 Always Encrypted 金鑰](configure-always-encrypted-keys-using-ssms.md)
- [使用 SQL Server Management Studio 輪替 Always Encrypted 金鑰](rotate-always-encrypted-keys-using-ssms.md)
- [使用 [Always Encrypted 精靈] 設定資料行加密](always-encrypted-wizard.md)
- [使用 Always Encrypted 與 DAC 套件設定資料行加密](configure-always-encrypted-using-dacpac.md)
- [使用 Always Encrypted 與 SQL Server Management Studio 查詢資料行](always-encrypted-query-columns-ssms.md)
- [使用 Always Encrypted 匯出和匯入資料庫](always-encrypted-migrate-using-bacpac.md)
- [使用 Always Encrypted 備份和還原資料庫](always-encrypted-migrate-using-backup-restore.md)
- [使用 Always Encrypted 與 SQL Server [匯入及匯出精靈]，將資料移轉進或移轉出資料行](always-encrypted-migrate-using-import-export-wizard.md)

## <a name="see-also"></a>另請參閱
- [一律加密](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [Always Encrypted 的金鑰管理概觀](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)
- [使用 PowerShell 設定 Always Encrypted](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md)
- [使用 Always Encrypted 開發應用程式](always-encrypted-client-development.md)
