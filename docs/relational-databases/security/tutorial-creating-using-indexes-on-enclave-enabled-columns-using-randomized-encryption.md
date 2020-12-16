---
title: 搭配隨機加密的已啟用記憶體保護區之資料行上的索引 (教學課程)
description: 此教學課程會指導您使用 SQL Server 具有安全記憶體保護區的 Always Encrypted 中所支援的隨機化加密，在已啟用記憶體保護區的資料行上建立及使用索引的方式。
ms.custom: seo-lt-2019
ms.date: 12/12/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.suite: sql
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: tutorial
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15'
ms.openlocfilehash: d8d3b67a8909867760b7ab01ebf860dd2f8dfe48
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97467219"
---
# <a name="tutorial-create-and-use-indexes-on-enclave-enabled-columns-using-randomized-encryption"></a>教學課程：使用隨機化加密在已啟用記憶體保護區的資料行上建立及使用索引
[!INCLUDE [sqlserver2019-windows-only](../../includes/applies-to-version/sqlserver2019-windows-only.md)]

本教學課程會指導您使用[具有安全記憶體保護區的 Always Encrypted](encryption/always-encrypted-enclaves.md) 中所支援的隨機化加密，在已啟用記憶體保護區的資料行上建立及使用索引的方式。 它會顯示：

- 如何在能夠存取保護資料行的金鑰 (資料行主要金鑰和資料行加密金鑰) 的情況下建立索引。
- 如何在無法存取保護資料行之金鑰的情況下建立索引。

## <a name="prerequisites"></a>Prerequisites

本教學課程是[教學課程：使用 SSMS，開始使用具有安全記憶體保護區的 Always Encrypted](./tutorial-getting-started-with-always-encrypted-enclaves.md)。 請確定您已完成它，再繼續進行下列步驟。

## <a name="step-1-enable-accelerated-database-recovery-adr-in-your-database"></a>步驟 1:在您的資料庫中啟用加速資料庫復原 (ADR)

Microsoft 強烈建議先在您的資料庫中啟用 ADR，再使用隨機化加密於已啟用記憶體保護區的資料行上建立第一個索引。 請參閱[具有安全記憶體保護區的 Always Encrypted](./encryption/always-encrypted-enclaves.md) 中的[＜資料庫復原＞](./encryption/always-encrypted-enclaves.md#database-recovery)一節。

1. 關閉您在上一個教學課程中所使用的任何 SSMS 執行個體。 這將會關閉您已開啟的資料庫連接；此為啟用 ADR 的必要條件。
1. 開啟新的 SSMS 執行個體，並在 **未** 針對資料庫連接啟用 Always Encrypted 的情況下，以 sysadmin 身分連線到 SQL Server 執行個體。
    1. 啟動 SSMS。
    1. 在 [連線到伺服器]  對話方塊中指定您的伺服器名稱，選取驗證方法，然後指定認證。
    1. 按一下 [選項 >>]  ，然後選取 [Always Encrypted]  索引標籤。
    1. 請確定 **未** 選取 [啟用 Always Encrypted (資料行加密)]  核取方塊。
    1. 選取 [連接]  。
1. 開啟新的查詢視窗並執行下列陳述式以啟用 ADR。

   ```sql
   ALTER DATABASE ContosoHR SET ACCELERATED_DATABASE_RECOVERY = ON;
   ```

## <a name="step-2-create-and-test-an-index-without-role-separation"></a>步驟 2:在未隔離角色的情況下建立並測試索引

在此步驟中，您將會建立並測試已加密資料行上的索引。 您將會以擔任 DBA、管理資料庫，以及具有保護資料之金鑰的資料擁有者等角色的單一使用者身分執行。

1. 開啟新的 SSMS 執行個體，並在 **已** 針對資料庫連接啟用 Always Encrypted 的情況下連線到 SQL Server 執行個體。
   1. 啟動新的 SSMS 執行個體。
   1. 在 [連線到伺服器]  對話方塊中指定您的伺服器名稱，選取驗證方法，然後指定認證。
   1. 按一下 [選項 >>]  ，然後選取 [Always Encrypted]  索引標籤。
   1. 選取 [啟用 Always Encrypted (資料行加密)]  核取方塊，然後指定您的記憶體保護區證明 URL (例如，ht<span>tp://<   span>hgs.bastion.local/Attestation)。
   1. 選取 [連接]  。
   1. 如果系統提示您啟用 Always Encrypted 的參數化查詢，按一下 [啟用]  。
1. 如果系統未提示您啟用 Always Encrypted 的參數化，請確認其已啟用。
   1. 從 SSMS 的主功能表選取 [工具]  。
   2. 選取 [選項]  。
   3. 瀏覽至 [查詢執行]   > [SQL Server]   > [進階]  。
   4. 確定已選取 [啟用 Always Encrypted 的參數化]  。
   5. 選取 [確定]  。
1. 開啟查詢視窗並執行下列陳述式，以將 **Employees** 資料表中的 **LastName** 資料行加密。 您將會在稍後的步驟中建立並使用該資料行上的索引。

   ```sql
   USE [ContosoHR];
   GO   
   ALTER TABLE [dbo].[Employees]
   ALTER COLUMN [LastName] [nvarchar](50) COLLATE Latin1_General_BIN2 
   ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = [CEK1], ENCRYPTION_TYPE = Randomized    ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL;
   GO   
   ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE;
   GO
   ```

1. 在 **LastName** 資料行上建立索引。 由於您是在啟用 Always Encrypted 的情況下連線到資料庫，SSMS 內的用戶端驅動程式會以透明方式向記憶體保護區提供 **CEK1** (保護 **LastName** 資料行的資料行加密金鑰)，其為建立索引的所需項目。

   ```sql
   USE [ContosoHR];
   GO

   CREATE INDEX IX_LastName ON [Employees] ([LastName])
   INCLUDE ([EmployeeID], [FirstName], [SSN], [Salary]);
   GO
   ```

1. 在 **LastName** 資料行上執行豐富查詢，並確認 SQL Server 在執行查詢時會使用該索引。
   1. 在相同的或新的查詢視窗中，確定工具列上的 [包含即時查詢統計資料]  按鈕已經開啟。
   1. 執行下列查詢。

       ```sql
       USE [ContosoHR];
       GO

       DECLARE @LastNamePrefix NVARCHAR(50) = 'Aber%';
       SELECT * FROM [dbo].[Employees] WHERE [LastName] LIKE @LastNamePrefix;
       GO
      ```

   1. 在 [即時查詢統計資料]  索引標籤 (位於查詢視窗的底部) 中，觀察查詢是否會使用索引。

## <a name="step-3-create-an-index-with-role-separation"></a>步驟 3：建立具有角色隔離的索引

在此步驟中，您將會在已加密的資料行上建立索引，並扮演兩個不同的使用者。 一個使用者是 DBA，其需要建立索引，但不具備金鑰的存取權。 另一個使用者是資料擁有者，其具備金鑰存取權。

1. 在 **未** 啟用 Always Encrypted 的情況下使用 SSMS 執行個體來執行下列陳述式，以在 **LastName** 資料行上放置索引。

   ```sql
   USE [ContosoHR];
   GO

   DROP INDEX IX_LastName ON [Employees]; 
   GO
   ```

1. 以資料擁有者的身分 (或是能存取金鑰的應用程式)，以 **CEK1** 填入記憶體保護區內的快取。

   > [!NOTE]
   > 除非您在 **步驟 2：在未隔離角色的情況下建立並測試索引** 之後曾重新啟動 SQL Server 執行個體，否則此步驟是不必要的，因為 **CEK1** 已經位於快取之中。 我們加入它的原因是為了示範資料擁有者如何在金鑰尚未存在於記憶體保護區中的情況下為它提供金鑰。

   1. 在 **已** 啟用 Always Encrypted 的 SSMS 執行個體中，於查詢視窗中執行下列陳述式。 該陳述式會將所有已啟用記憶體保護區之資料行的加密金鑰傳送到記憶體保護區。 請參閱 [sp_enclave_send_keys](../system-stored-procedures/sp-enclave-send-keys-sql.md) 以取得詳細資料。

        ```sql
        USE [ContosoHR];
        GO

        EXEC sp_enclave_send_keys;
        GO
        ```

   1. 作為執行上述預存程序的替代方案，您也可以執行會針對 **LastName** 資料行使用記憶體保護區的 DML 查詢。 這將會僅搭配 **CEK1** 來填入記憶體保護區。

        ```sql
        USE [ContosoHR];
        GO

        DECLARE @LastNamePrefix NVARCHAR(50) = 'Aber%';
        SELECT * FROM [dbo].[Employees] WHERE [LastName] LIKE @LastNamePrefix;
        GO
        ```

1. 以 DBA 的身分建立索引。
    1. 在 **未** 啟用 Always Encrypted 的 SSMS 執行個體中，於查詢視窗中執行下列陳述式。

        ```sql
        USE [ContosoHR];
        GO

        CREATE INDEX IX_LastName ON [Employees] ([LastName])
        INCLUDE ([EmployeeID], [FirstName], [SSN], [Salary]);
        GO
        ```

1. 以資料擁有者的身分，在 **LastName** 資料行上執行豐富查詢，並確認 SQL Server 在執行查詢時會使用該索引。
   1. 在 **已** 啟用 Always Encrypted 的 SSMS 執行個體中，選取現有的查詢視窗或開啟新的查詢視窗，並確定工具列上的 [包含即時查詢統計資料]  按鈕已經開啟。
   1. 執行下列查詢。 

        ```sql
        USE [ContosoHR];
        GO

        DECLARE @LastNamePrefix NVARCHAR(50) = 'Aber%';
        SELECT * FROM [dbo].[Employees] WHERE [LastName] LIKE @LastNamePrefix;
        GO
        ```

   1. 在 [即時查詢統計資料]  (位於查詢視窗的底部) 中，觀察查詢是否會使用索引。

## <a name="next-steps"></a>後續步驟
- [教學課程：使用具有安全記憶體保護區的 Always Encrypted 開發 .NET Framework 應用程式](tutorial-always-encrypted-enclaves-develop-net-framework-apps.md)

## <a name="see-also"></a>另請參閱
- [使用具有安全記憶體保護區的 Always Encrypted 在資料行上建立及使用索引](encryption/always-encrypted-enclaves-create-use-indexes.md)
