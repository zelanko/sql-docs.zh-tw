---
title: "實作組件 |Microsoft 文件"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: clr
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords: assemblies [CLR integration], implementing
ms.assetid: c228d7bf-a906-4f37-a057-5d464d962ff8
caps.latest.revision: "33"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: dadb7fe14a03bfd94350ea280cca94494e3c163b
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="assemblies---implementing"></a>-實作組件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]本主題提供有關下列領域，可協助您實作和使用資料庫中的組件的資訊：  
  
-   建立組件  
  
-   修改組件  
  
-   卸除、停用和啟用組件  
  
-   管理組件版本  
  
## <a name="creating-assemblies"></a>建立組件  
 組件是使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CREATE ASSEMBLY 陳述式在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中建立，或使用 Assembly Assisted Editor 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中建立。 此外，SQL Server 中部署專案[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]已指定給專案的資料庫中註冊組件。 如需詳細資訊，請參閱 [Deploying CLR Database Objects](../../relational-databases/clr-integration/deploying-clr-database-objects.md)。  
  
 **若要使用 TRANSACT-SQL 建立組件**  
  
-   [CREATE ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/create-assembly-transact-sql.md)  
  
 **若要使用 SQL Server Management Studio 建立組件**  
  
-   [組件屬性 &#40;一般頁面 &#41;](../../relational-databases/clr-integration/assemblies-properties.md)  
  
## <a name="modifying-assemblies"></a>修改組件  
 組件是使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ALTER ASSEMBLY 陳述式在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中修改，或使用 Assembly Assisted Editor 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中修改。 當您要執行下列動作時可以修改組件：  
  
-   上傳較新版的二進位編碼檔案組件，以變更組件的實作。 如需詳細資訊，請參閱[管理組件版本](#_managing)本主題稍後。  
  
-   變更組件的權限集。 如需詳細資訊，請參閱[設計組件](../../relational-databases/clr-integration/assemblies-designing.md)。  
  
-   變更組件的可見性。 可見的組件可在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中用來參考。 看不見的組件則無法使用，即使已在資料庫中上傳它們也一樣。 依預設，上傳至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的組件是可見的。  
  
-   加入或卸除與組件關聯的偵錯或來源檔。  
  
 **若要使用 TRANSACT-SQL 修改組件**  
  
-   [ALTER ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-assembly-transact-sql.md)  
  
 **若要使用 SQL Server Management Studio 修改組件**  
  
-   [組件屬性 &#40;一般頁面 &#41;](../../relational-databases/clr-integration/assemblies-properties.md)  
  
## <a name="dropping-disabling-and-enabling-assemblies"></a>卸除、停用和啟用組件  
 使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] DROP ASSEMBLY 陳述式或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 卸除組件。  
  
 **若要使用 TRANSACT-SQL 卸除組件**  
  
-   [DROP ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-assembly-transact-sql.md)  
  
 **若要使用 SQL Server Management Studio 卸除組件**  
  
-   [刪除物件](http://msdn.microsoft.com/library/49541441-179c-40d3-ba0c-01bcae545984)  
  
 依預設，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中建立的所有組件都會停用執行。 您可以使用**clr 已啟用**選項**sp_configure**系統預存程序來停用或啟用的所有組件中上傳執行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 停用組件的執行可防止執行 Common Language Runtime (CLR) 函數、預存程序、觸發程序、彙總和使用者定義型別，並可停止那些正在執行的。 停用組件的執行並不會停用建立、修改或卸除組件的功能。 如需詳細資訊，請參閱[clr 已啟用伺服器組態選項](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md)。  
  
 **若要停用和啟用組件的執行**  
  
-   [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
##  <a name="_managing"></a>管理組件版本  
 在將組件上傳至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體時，組件是在資料庫系統目錄中儲存和管理。 中的組件定義所做的任何變更[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]應該傳播至儲存在資料庫目錄中的組件。  
  
 當您必須修改組件時，您必須發出 ALTER ASSEMBLY 陳述式來更新資料庫中的組件。 這將會使組件更新至保存其實作的最新 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 模組副本。  
  
 ALTER ASSEMBLY 陳述式的 WITH UNCHECKED DATA 子句可指示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 重新整理那些甚至是與在資料庫中的保存資料相依之組件。 特別是，如果下列任一項存在，您就必須指定 WITH UNCHECKED DATA：  
  
-   透過 [!INCLUDE[tsql](../../includes/tsql-md.md)] 函數或方法直接或間接參考組件中的方法之保存的計算資料行。  
  
-   CLR 使用者定義型別的相依於組件和型別實作的資料行**UserDefined** (非**原生**) 序列化格式。  
  
> [!CAUTION]  
>  在未指定 WITH UNCHECKED DATA 的情況下，如果新組件版本影響資料表、索引或其他永續性站台中現有的資料，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 將嘗試阻止 ALTER ASSEMBLY 執行。 不過，當 CLR 組件更新時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 並不保證計算資料行、索引、索引檢視或運算式都會與基礎常式及類型保持一致。 執行 ALTER ASSEMBLY 時請小心，以確定運算式結果與儲存在組件中以該運算式為基礎的值之間相符。  
  
 只有成員**db_owner**和**db_ddlowner**固定的資料庫角色可以執行使用 WITH UNCHECKED DATA 子句執行 ALTER ASSEMBLY。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會在 Windows 應用程式事件記錄公佈訊息，說明已使用資料表中未檢查的資料修改過組件。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 接著會在有未檢查的資料時，標示任何包含與組件相依的資料之資料表。 **Has_unchecked_assembly_data**資料行**sys.tables**目錄檢視包含資料表，其中包含未選取的資料，以 0 代表沒有未檢查資料的值 1。  
  
 若要解決未檢查資料的完整性，請針對具有每個資料表執行 DBCC CHECKDB WITH EXTENDED_LOGICAL_CHECKS 未檢查的資料。 如果 DBCC CHECKDB WITH EXTENDED_LOGICAL_CHECKS 失敗，則必須刪除無效或修改的組件程式碼，來解決問題的資料表資料列，並接著發出其他 ALTER ASSEMBLY 陳述式。  
  
 ALTER ASSEMBLY 會變更組件版本。 文化特性和公開金鑰語彙基元的組件則維持不變。SQL Server 不允許註冊具有相同名稱、 文化特性和公開金鑰的組件的不同版本。  
  
### <a name="interactions-with-computer-wide-policy-for-version-binding"></a>與版本繫結的電腦通用原則互動  
 如果儲存在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的組件參考，使用簽發者原則或電腦通用管理原則重新導向至特定版本，您必須執行下列其中一個動作：  
  
-   請確定是在資料庫中執行導向至新版本。  
  
-   請修改任何對於電腦或簽發者原則的外部原則檔案之陳述式，以確定它們所參考的特定版本是在資料庫中。  
  
 否則，嘗試載入新組件版本至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體將會失敗。  
  
 **若要更新的組件版本**  
  
-   [ALTER ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-assembly-transact-sql.md)  
  
## <a name="see-also"></a>請參閱＜  
 [組件 &#40; Database engine&#41;](../../relational-databases/clr-integration/assemblies-database-engine.md)   
 [取得組件的相關資訊](../../relational-databases/clr-integration/assemblies-getting-information.md)  
  
  
