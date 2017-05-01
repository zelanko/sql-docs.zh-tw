---
title: "永遠加密的金鑰管理概觀 | Microsoft Docs"
ms.custom: 
ms.date: 07/20/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-security
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 07a305b1-4110-42f0-b7aa-28a4e32e912a
caps.latest.revision: 32
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 611fcbd96531e57dd47a7ae61e5b4b32d84dcb46
ms.lasthandoff: 04/11/2017

---
# <a name="overview-of-key-management-for-always-encrypted"></a>永遠加密的金鑰管理概觀
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]


[永遠加密](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)使用兩種密碼編譯金鑰類型來保護您的資料 - 一種金鑰用來加密您的資料，而另一種金鑰則用來對加密資料的金鑰進行加密。 資料行加密金鑰會加密您的資料，而資料行主要金鑰則會加密資料行加密金鑰。 本文提供詳細概觀來說明如何管理這些加密金鑰。

當討論到永遠加密金鑰和金鑰管理時，請務必了解實際的密碼編譯金鑰與「描述」金鑰的中繼資料物件之間的差異。 我們使用**資料行加密金鑰**和**資料行主要金鑰**等詞彙來表示實際的密碼編譯金鑰，並使用**資料行加密金鑰中繼資料**和**資料行主要金鑰中繼資料**來表示資料庫中的永遠加密金鑰「描述」。

- 「資料行加密金鑰」是用來加密資料的內容加密金鑰。 顧名思義，您可以使用資料行加密金鑰來加密資料庫資料行中的資料。 您可以使用相同的資料行加密金鑰來加密一或多個資料行，或根據您的應用程式需求，使用多個資料行加密金鑰。 資料行加密金鑰本身經過加密，只有資料行加密金鑰的加密值會儲存在資料庫中 (當作資料行加密金鑰中繼資料的一部分)。 資料行加密金鑰中繼資料則會儲存在 [sys.column_encryption_keys (TRANSACT-SQL)](../../../relational-databases/system-catalog-views/sys-column-encryption-keys-transact-sql.md) 和 [sys.column_encryption_key_values (TRANSACT-SQL)](../../../relational-databases/system-catalog-views/sys-column-encryption-key-values-transact-sql.md) 目錄檢視中。 搭配 AES-256 演算法使用之資料行加密金鑰的長度為 256 位元。


- 「資料行主要金鑰」是用來加密資料行加密金鑰的金鑰保護型金鑰。 資料行主要金鑰必須儲存在受信任的金鑰存放區中，例如 Windows 憑證存放區、Azure 金鑰保存庫或硬體安全模組。 資料庫只會包含資料行主要金鑰的相關中繼資料 (金鑰存放區類型和位置)。 資料行主要金鑰中繼資料則會儲存在 [sys.column_master_keys (TRANSACT-SQL)](../../../relational-databases/system-catalog-views/sys-column-master-keys-transact-sql.md) 目錄檢視中。  

請務必注意，資料庫系統中的金鑰中繼資料不包含純文字資料行主要金鑰或純文字資料行加密金鑰。 資料庫只會包含資料行主要金鑰類型和位置的相關資訊，以及資料行加密金鑰的加密值。 這表示永遠不會向資料庫系統公開純文字金鑰，如此可確保使用永遠加密保護的資料安全無虞，即使資料庫系統遭到入侵亦然。 若要確保資料庫系統無法存取純文字金鑰，請務必在與裝載您的資料庫不同的電腦上執行金鑰管理工具 - 如需詳細資訊，請參閱下面的 [金鑰管理的安全性考量](#SecurityForKeyManagement) 一節。

因為資料庫只會包含加密資料 (在受永遠加密保護的資料行中)，而且無法存取純文字金鑰，所以無法解密資料。 這表示查詢永遠加密的資料行只會傳回加密值，因此需要加密或解密受保護資料的用戶端應用程式必須能夠存取資料行主要金鑰，以及相關的資料行加密金鑰。 如需詳細資訊，請參閱 [永遠加密 (用戶端開發)](../../../relational-databases/security/encryption/always-encrypted-client-development.md)。



## <a name="key-management-tasks"></a>金鑰管理工作

管理金鑰的程序可分為下列高階工作：

- **金鑰佈建** - 在受信任的金鑰存放區 (例如 Windows 憑證存放區、Azure 金鑰保存庫或硬體安全模組) 中建立實體金鑰；使用資料行主要金鑰來加密資料行加密金鑰；以及在資料庫中建立這兩種金鑰類型的中繼資料。

- **金鑰輪替** - 定期以新的金鑰更換現有的金鑰。 如果金鑰已遭洩漏，或是為了符合您的組織原則或必須更換授權密碼編譯金鑰的標準規定，您可能必須更換金鑰。 


## <a name="KeyManagementRoles"></a> 金鑰管理角色

管理永遠加密金鑰的使用者有兩種不同的角色：安全性系統管理員和資料庫管理員 (DBA)：

- **安全性系統管理員** - 產生資料行加密金鑰和資料行主要金鑰，以及管理包含資料行主要金鑰的金鑰存放區。 若要執行這些工作，安全性系統管理員必須能夠存取金鑰和金鑰存放區，但不需要資料庫的存取權。
- **DBA** - 管理資料庫中金鑰的相關中繼資料。 若要執行金鑰管理工作，DBA 必須能管理資料庫中的金鑰中繼資料，但不需要金鑰或保留資料行主要金鑰之金鑰存放區的存取權。

就上述角色而言，執行永遠加密之金鑰管理工作的方式有兩種： *使用角色隔離*和 *不使用角色隔離*。 您可以根據組織的需求，選擇最適合您需求的金鑰管理程序。

## <a name="managing-keys-with-role-separation"></a>使用角色隔離管理金鑰
使用角色隔離管理永遠加密金鑰時，會由組織中的不同人員擔任安全性系統管理員和 DBA 角色。 使用角色隔離的金鑰管理程序可確保 DBA 無法存取金鑰或保留實際金鑰的金鑰存放區，且安全性系統管理員無法存取包含敏感性資料的資料庫。 如果您的目標是確保組織中的 DBA 無法存取敏感性資料，建議使用角色隔離管理金鑰。 

**注意：** 安全性系統管理員會產生並處理純文字金鑰，因此永遠都不應該在裝載資料庫系統的相同電腦，或是 DBA 或其他可能成為潛在敵人之任何人可存取的電腦上執行其工作。 

## <a name="managing-keys-without-role-separation"></a>不使用角色隔離管理金鑰
不使用角色隔離管理永遠加密金鑰時，某個人員可同時擔任安全性系統管理員和 DBA 角色，這表示該人員必須能夠存取及管理金鑰/金鑰存放區和金鑰中繼資料。 針對使用 DevOps 模型的組織，或是如果資料庫裝載於雲端且主要目標是限制雲端管理員 (而不是內部部署 DBA) 存取敏感性資料，可建議不使用角色隔離來管理金鑰。



## <a name="tools-for-managing-always-encrypted-keys"></a>管理永遠加密金鑰的工具

永遠加密金鑰可透過 [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/ms174173.aspx) 和 [PowerShell](https://msdn.microsoft.com/library/hh245198.aspx)進行管理：

- **SQL Server Management Studio (SSMS)** - 提供結合與金鑰存放區存取和資料庫存取相關之工作的對話方塊和精靈，因此 SSMS 雖然不支援角色隔離，但可讓您輕鬆地設定金鑰。 如需使用 SSMS 管理金鑰的詳細資訊，請參閱：
    - [佈建資料行主要金鑰](../../../relational-databases/security/encryption/configure-always-encrypted-using-sql-server-management-studio.md#provisioncmk)
    - [佈建資料行加密金鑰](../../../relational-databases/security/encryption/configure-always-encrypted-using-sql-server-management-studio.md#provisioncek)
    - [輪替資料行主要金鑰](../../../relational-databases/security/encryption/configure-always-encrypted-using-sql-server-management-studio.md#rotatecmk)
    - [輪替資料行加密金鑰](../../../relational-databases/security/encryption/configure-always-encrypted-using-sql-server-management-studio.md#rotatecek)


- **SQL Server PowerShell** - 包含以使用和不使用角色隔離來管理永遠加密金鑰的 Cmdlet。 如需詳細資訊，請參閱：
    - [使用 PowerShell 設定永遠加密金鑰](../../../relational-databases/security/encryption/configure-always-encrypted-keys-using-powershell.md)
    - [使用 PowerShell 更換永遠加密金鑰](../../../relational-databases/security/encryption/rotate-always-encrypted-keys-using-powershell.md)


## <a name="SecurityForKeyManagement"></a> 金鑰管理的安全性考量

永遠加密的主要目標是為了確保儲存在資料庫中的敏感性資料安全無虞，即使資料庫系統或其主控環境遭到入侵亦然。 永遠加密可協助防止敏感性資料外洩的安全性攻擊範例包括：

- 惡意的高權限資料庫使用者 (例如 DBA) 查詢敏感性資料行。
- 裝載 SQL Server 執行個體之電腦的惡意系統管理員掃描 SQL Server 處理序記憶體，或 SQL Server 處理序傾印檔案。
- 惡意的資料中心操作員查詢客戶資料庫、檢查 SQL Server 傾印檔案，或檢查在雲端中裝載客戶資料之電腦的記憶體。
- 裝載資料庫之電腦上執行的惡意程式碼。

為了確保永遠加密能夠有效地防止這類攻擊，您的金鑰管理程序必須確保資料行主要金鑰和資料行加密金鑰，以及包含資料行主要金鑰的金鑰存放區認證永遠不會洩漏給潛在攻擊者。 以下是您應該遵循的一些方針：

- 永遠不要在裝載您資料庫的電腦上產生資料行主要金鑰或資料行加密金鑰。 請改為在不同的電腦上產生金鑰，這些電腦可以是金鑰管理的專用電腦，或是裝載無論如何都必須存取金鑰之應用程式的電腦。 這表示 **您永遠都不應該在裝載資料庫的電腦上執行用來產生金鑰的工具** ，因為如果攻擊者存取用來佈建或維護永遠加密金鑰的電腦，攻擊者可能會取得您的金鑰，即使金鑰只短暫地出現在工具的記憶體中亦然。
- 為了確保您的金鑰管理程序不會不小心洩露資料行主要金鑰或資料行加密金鑰，請務必識別潛在敵人和安全性威脅，再定義及實作金鑰管理程序。 例如，如果您的目標是為了確保 DBA 無法存取敏感性資料，則不能由 DBA 負責產生金鑰。 不過，DBA「可以」管理資料庫中的金鑰中繼資料，因為中繼資料不包含純文字金鑰。

## <a name="next-steps"></a>後續步驟

- [建立及儲存資料行主要金鑰 (永遠加密)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)
- [使用 PowerShell 設定永遠加密金鑰](../../../relational-databases/security/encryption/configure-always-encrypted-keys-using-powershell.md)
- [使用 PowerShell 輪替永遠加密金鑰](../../../relational-databases/security/encryption/rotate-always-encrypted-keys-using-powershell.md)
- [使用 SQL Server Management Studio 設定永遠加密](../../../relational-databases/security/encryption/configure-always-encrypted-using-sql-server-management-studio.md)

## <a name="additional-resources"></a>其他資源

- [一律加密 (Database Engine)](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [Always Encrypted (Client Development)](../../../relational-databases/security/encryption/always-encrypted-client-development.md)
- [永遠加密精靈教學課程 (Azure 金鑰保存庫)](https://azure.microsoft.com/documentation/articles/sql-database-always-encrypted-azure-key-vault/)
- [永遠加密精靈教學課程 (Windows 憑證存放區)](https://azure.microsoft.com/documentation/articles/sql-database-always-encrypted/)





