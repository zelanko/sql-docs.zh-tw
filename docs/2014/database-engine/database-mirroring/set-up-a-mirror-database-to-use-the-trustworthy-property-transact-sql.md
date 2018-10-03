---
title: 設定鏡像資料庫可使用 Trustworthy 屬性 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- TRUSTWORTHY database option
- mirror database [SQL Server]
- database mirroring [SQL Server], security
ms.assetid: 6993b076-78ef-453e-b0ea-e341b8e5ee3e
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 29cafc7e9669ca322571ff171961dd64cab114cf
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48069508"
---
# <a name="set-up-a-mirror-database-to-use-the-trustworthy-property-transact-sql"></a>設定鏡像資料庫可使用 Trustworthy 屬性 (Transact-SQL)
  備份資料庫時，TRUSTWORTHY 資料庫屬性將設為 OFF。 因此，新鏡像資料庫上的 TRUSTWORTHY 一律為 OFF。 您必須在鏡像開始之後執行額外的設定步驟，以確保資料庫在容錯移轉之後的可信度。  
  
> [!NOTE]  
>  如需此資料庫屬性的相關資訊，請參閱 [TRUSTWORTHY 資料庫屬性](../../relational-databases/security/trustworthy-database-property.md)。  
  
## <a name="procedure"></a>程序  
  
#### <a name="to-setup-a-mirror-database-to-use-the-trustworthy-property"></a>若要設定鏡像資料庫以使用 Trustworthy 屬性  
  
1.  在主體伺服器執行個體上，確認主體資料庫是否已開啟 Trustworthy 屬性。  
  
    ```  
    SELECT name, database_id, is_trustworthy_on FROM sys.databases   
    ```  
  
     如需詳細資訊，請參閱 [sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)。  
  
2.  啟動鏡像之後，請確認資料庫目前是否為主體資料庫、工作階段是否使用同步作業模式，以及工作階段是否已同步處理。  
  
    ```  
    SELECT database_id, mirroring_role, mirroring_safety_level_desc, mirroring_state_desc FROM sys.database_mirroring  
    ```  
  
     如需詳細資訊，請參閱 [sys.database_mirroring &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-mirroring-transact-sql)。  
  
3.  同步處理鏡像工作階段之後，請以手動方式執行容錯移轉，將工作交給鏡像資料庫。  
  
     您可以在 SQL Server Management Studio 中或使用 Transact-SQL 執行此動作：  
  
    -   [手動容錯移轉資料庫鏡像工作階段 &#40;SQL Server Management Studio&#41;](manually-fail-over-a-database-mirroring-session-sql-server-management-studio.md)  
  
    -   [手動容錯移轉資料庫鏡像工作階段 &#40;Transact-SQL&#41;](manually-fail-over-a-database-mirroring-session-transact-sql.md)  
  
4.  使用下列 ALTER DATABASE 命令開啟 Trustworthy 資料庫屬性：  
  
    ```  
    ALTER DATABASE <database_name> SET TRUSTWORTHY ON  
    ```  
  
     如需詳細資訊，請參閱 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)。  
  
5.  您可以選擇性地再次以手動方式進行容錯移轉，將工作交回給原始主體。  
  
6.  您可以選擇性地將 SAFETY 設定為 OFF，並確認 WITNESS 也設為 OFF，以便切換到非同步的高效能模式。  
  
     在 Transact-SQL 中：  
  
    -   [變更資料庫鏡像工作階段中的異動安全性 &#40;Transact-SQL&#41;](change-transaction-safety-in-a-database-mirroring-session-transact-sql.md)  
  
    -   [從資料庫鏡像工作階段移除見證 &#40;SQL Server&#41;](remove-the-witness-from-a-database-mirroring-session-sql-server.md)  
  
     在 SQL Server Management Studio 中：  
  
    -   [使用 Windows 驗證建立資料庫鏡像工作階段 &#40;SQL Server Management Studio&#41;](establish-database-mirroring-session-windows-authentication.md)  
  
## <a name="see-also"></a>另請參閱  
 [TRUSTWORTHY 資料庫屬性](../../relational-databases/security/trustworthy-database-property.md)   
 [設定加密鏡像資料庫](set-up-an-encrypted-mirror-database.md)  
  
  
