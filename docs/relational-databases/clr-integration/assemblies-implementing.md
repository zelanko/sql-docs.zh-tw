---
title: 實施程式集 |微軟文件
description: 瞭解如何使用 SQL Server 上託管的程式集,包括如何創建/修改程式集、刪除或啟用/禁用程式集以及管理版本。
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- assemblies [CLR integration], implementing
ms.assetid: c228d7bf-a906-4f37-a057-5d464d962ff8
author: rothja
ms.author: jroth
ms.openlocfilehash: 807ed6a6f0d59444cd38f7fdf902a7c3fc1b47d8
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2020
ms.locfileid: "81488039"
---
# <a name="assemblies---implementing"></a>組件 - 實作
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  本主題提供下列部分的資訊，協助您實作和使用資料庫中的組件：  
  
-   建立組件  
  
-   修改組件  
  
-   卸除、停用和啟用組件  
  
-   管理組件版本  
  
## <a name="creating-assemblies"></a>建立組件  
 組件是使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CREATE ASSEMBLY 陳述式在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中建立，或使用 Assembly Assisted Editor 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中建立。 此外,在[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]資料庫中部署 SQL Server 專案會註冊為專案指定的程式集。 如需詳細資訊，請參閱 [Deploying CLR Database Objects](../../relational-databases/clr-integration/deploying-clr-database-objects.md)。  
  
 **若要使用 Transact-SQL 建立組件**  
  
-   [CREATE ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/create-assembly-transact-sql.md)  
  
 **若要使用 SQL Server Management Studio 建立組件**  
  
-   [裝配屬性&#40;常規頁面&#41;](../../relational-databases/clr-integration/assemblies-properties.md)  
  
## <a name="modifying-assemblies"></a>修改組件  
 組件是使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ALTER ASSEMBLY 陳述式在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中修改，或使用 Assembly Assisted Editor 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中修改。 當您要執行下列動作時可以修改組件：  
  
-   上傳較新版的二進位編碼檔案組件，以變更組件的實作。 有關詳細資訊,請參閱本主題後面的[管理程式集版本](#_managing)。  
  
-   變更組件的權限集。 如需詳細資訊，請參閱[設計組件](../../relational-databases/clr-integration/assemblies-designing.md)。  
  
-   變更組件的可見性。 可見的組件可在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中用來參考。 看不見的組件則無法使用，即使已在資料庫中上傳它們也一樣。 依預設，上傳至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的組件是可見的。  
  
-   加入或卸除與組件關聯的偵錯或來源檔。  
  
 **若要使用 Transact-SQL 修改組件**  
  
-   [ALTER ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-assembly-transact-sql.md)  
  
 **若要使用 SQL Server Management Studio 修改組件**  
  
-   [裝配屬性&#40;常規頁面&#41;](../../relational-databases/clr-integration/assemblies-properties.md)  
  
## <a name="dropping-disabling-and-enabling-assemblies"></a>卸除、停用和啟用組件  
 使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] DROP ASSEMBLY 陳述式或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 卸除組件。  
  
 **若要使用 Transact-SQL 卸除組件**  
  
-   [DROP ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-assembly-transact-sql.md)  
  
 **若要使用 SQL Server Management Studio 卸除組件**  
  
-   [刪除物件](../../ssms/object/delete-objects.md)  
  
 依預設，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中建立的所有組件都會停用執行。 您可以使用**sp_configure**系統儲存過程[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的啟用**clr**選項來禁用或啟用在 中上載的所有程式集的執行。 停用組件的執行可防止執行 Common Language Runtime (CLR) 函數、預存程序、觸發程序、彙總和使用者定義型別，並可停止那些正在執行的。 停用組件的執行並不會停用建立、修改或卸除組件的功能。 關於詳細資訊,請參閱啟用[clr 的伺服器設定選項](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md)。  
  
 **若要停用和啟用組件執行**  
  
-   [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
##  <a name="managing-assembly-versions"></a><a name="_managing"></a>管理程式集版本  
 在將組件上傳至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體時，組件是在資料庫系統目錄中儲存和管理。 對中的程式集[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]定義所做的任何更改都應傳播到存儲在資料庫目錄中的程式集。  
  
 當您必須修改組件時，您必須發出 ALTER ASSEMBLY 陳述式來更新資料庫中的組件。 這將會使組件更新至保存其實作的最新 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 模組副本。  
  
 ALTER ASSEMBLY 陳述式的 WITH UNCHECKED DATA 子句可指示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 重新整理那些甚至是與在資料庫中的保存資料相依之組件。 特別是，如果下列任一項存在，您就必須指定 WITH UNCHECKED DATA：  
  
-   透過 [!INCLUDE[tsql](../../includes/tsql-md.md)] 函數或方法直接或間接參考組件中的方法之保存的計算資料行。  
  
-   相依於組件的 CLR 使用者定義型別資料行，以及實作 **UserDefined** (非**原生**) 序列化格式之類型的資料行。  
  
> [!CAUTION]  
>  在未指定 WITH UNCHECKED DATA 的情況下，如果新組件版本影響資料表、索引或其他永續性站台中現有的資料，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 將嘗試阻止 ALTER ASSEMBLY 執行。 不過，當 CLR 組件更新時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 並不保證計算資料行、索引、索引檢視或運算式都會與基礎常式及類型保持一致。 執行 ALTER ASSEMBLY 時請小心，以確定運算式結果與儲存在組件中以該運算式為基礎的值之間相符。  
  
 只有**db_owner**和**db_ddlowner固定**資料庫角色的成員才能使用「UNCHECKED 資料」子句執行運行 ALTER ASSEMBLY。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會在 Windows 應用程式事件記錄公佈訊息，說明已使用資料表中未檢查的資料修改過組件。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 接著會在有未檢查的資料時，標示任何包含與組件相依的資料之資料表。 **sys.tables**目錄**檢視的has_unchecked_assembly_data**欄包含包含未檢查資料的表的值 1,包含沒有未檢查資料的表的值為 0。  
  
 要解決未檢查數據的完整性,請針對具有未檢查數據的每個表運行 DBCC CHECKDB,EXTENDED_LOGICAL_CHECKS。 如果 DBCC CHECKDB EXTENDED_LOGICAL_CHECKS失敗,則必須刪除無效的表行或修改程式集代碼以解決問題,然後發出其他 ALTER ASSEMBLY 語句。  
  
 ALTER ASSEMBLY 會變更組件版本。 程式集的區域性和公開權標記保持不變。SQL Server 不允許註冊具有相同名稱、區域性和公開金鑰的程式集的不同版本。  
  
### <a name="interactions-with-computer-wide-policy-for-version-binding"></a>與版本繫結的電腦通用原則互動  
 如果儲存在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的組件參考，使用簽發者原則或電腦通用管理原則重新導向至特定版本，您必須執行下列其中一個動作：  
  
-   請確定是在資料庫中執行導向至新版本。  
  
-   請修改任何對於電腦或簽發者原則的外部原則檔案之陳述式，以確定它們所參考的特定版本是在資料庫中。  
  
 否則，嘗試載入新組件版本至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體將會失敗。  
  
 **更新組件的版本**  
  
-   [ALTER ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-assembly-transact-sql.md)  
  
## <a name="see-also"></a>另請參閱  
 [程式集&#40;資料庫引擎&#41;](../../relational-databases/clr-integration/assemblies-database-engine.md)   
 [取得組件的相關資訊](../../relational-databases/clr-integration/assemblies-getting-information.md)  
  
  
