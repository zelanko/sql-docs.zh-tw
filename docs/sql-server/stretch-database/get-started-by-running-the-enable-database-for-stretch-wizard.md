---
title: 開始執行啟用資料庫的延展功能精靈
ms.date: 08/05/2016
ms.service: sql-server-stretch-database
ms.reviewer: ''
ms.topic: quickstart
f1_keywords:
- sql13.swb.stretchwizard.f1
- sql13.swb.stretchwizard.createdatabasecredentials.f1
- sql13.swb.stretchwizard.selectdatabasetables.f1
- sql13.swb.stretchwizard.validatesqlserver.f1
- sql13.swb.stretchwizard.selectazuredeployment.f1
- sql13.swb.stretchwizard.configureazuredeployment.f1
- sql13.swb.stretchwizard.Summary.f1
- sql13.swb.stretchwizard.Results.f1
- sql13.swb.stretchwizard.introduction.f1
helpviewer_keywords:
- Stretch Database, wizard
- Enable Database for Stretch Wizard
ms.assetid: 855dd9fc-f80c-4dbc-bf46-55a9736bfe15
author: rothja
ms.author: jroth
ms.custom: seo-dt-2019
ms.openlocfilehash: 5d730c8e71044154b9844174ac8d21837c9ea05f
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "73843796"
---
# <a name="get-started-by-running-the-enable-database-for-stretch-wizard"></a>開始執行啟用資料庫的延展功能精靈
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly.md)]


 若要設定資料庫以使用 Stretch Database，請執行「啟用資料庫的延展功能精靈」。  本文描述您必須輸入的資訊，以及必須在精靈中進行的選擇。  
  
 若要深入了解 Stretch Database，請參閱 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)。 
 
 > [!NOTE] 
 > 稍後，如果您停用 Stretch Database，請記住針對資料表或資料庫停用 Stretch Database，並不會刪除遠端物件。 若您想要刪除遠端資料表或遠端資料庫，則必須使用 Azure 管理入口網站將其卸除。 遠端物件會繼續產生 Azure 成本，直到您手動將其刪除為止。 
  
## <a name="launch-the-wizard"></a>啟動精靈  
  
1.  在 SQL Server Management Studio 的 [物件總管] 中，選取要啟用 Stretch 的資料庫。  
  
2.  按一下滑鼠右鍵並選取 [工作]  ，然後依序選取 [Stretch]  和 [啟用]  ，來啟動精靈。  
  
##  <a name="Intro"></a> 簡介  
 檢閱精靈的用途及必要條件。  
 
 以下是重要的必要條件。
 -   您必須是系統管理員才能變更資料庫設定。
 -   您必須有 Microsoft Azure 訂用帳戶。
 -   SQL Server 必須能夠與遠端的 Azure 伺服器通訊。
  
 ![Stretch Database 精靈的 [簡介] 頁面](../../sql-server/stretch-database/media/stretch-wizard-1.png "Stretch Database 精靈的 [簡介] 頁面")  
  
##  <a name="Tables"></a> 選取資料表  
 選取想要啟用延伸功能的資料表。  
 
有大量資料列的資料表會出現在排序清單的頂端。 精靈顯示資料表清單之前，它會針對 Stretch Database 目前不支援的資料類型分析它們。 
  
 ![Stretch Database 精靈的 [選取資料表] 頁面](../../sql-server/stretch-database/media/stretch-wizard-2.png "Stretch Database 精靈的 [選取資料表] 頁面")  
  
|資料行|描述|  
|------------|-----------------|  
|(沒有標題)|請勾選此資料欄的核取方塊，以為選取的資料表啟用延伸功能。|  
|**名稱**|指定資料庫中資料表的名稱。|  
|(沒有標題)|這個資料行中的符號可能代表警告，您仍然可以選取 Stretch 的資料表。 它也可能代表封鎖的問題，使您無法選取 Stretch 的資料表，比方說，因為資料表使用不支援的資料類型。 將滑鼠停留在工具提示中的符號上，來顯示詳細資訊。 如需詳細資訊，請參閱 [Stretch Database 的限制](../../sql-server/stretch-database/limitations-for-stretch-database.md)。|  
|**已延展**|指出資料表是否已經針對 Stretch 啟用。|  
|**移轉**|您可以移轉整個資料表 (**整份資料表**)，或者您可以指定篩選資料表中現有的資料行。 如果您想要使用不同的篩選函數來選取要移轉的資料列，請在結束精靈之後執行 ALTER TABLE 陳述式來指定篩選函數。 如需有關篩選函數的詳細資訊，請參閱 [Select rows to migrate by using a filter function](../../sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md)(使用篩選函數選取要移轉的資料列)。 如需如何套用函數的詳細資訊，請參閱[為資料表啟用 Stretch Database](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md) 或 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)。|  
|**資料列**|指定資料表中的資料列數目。|  
|**大小 (KB)**|指定資料表的大小 (KB)。|  
  
## <a name="optionally-provide-a-row-filter"></a>選擇性地提供資料列篩選  
 如果您想要提供篩選函數來選取要移轉的資料列，請在 [選取資料表]  頁面執行下列其中一項操作。  
  
1.  在 [選取要延展的資料表]  清單中，按一下資料表之資料列中的 [整份資料表]  。 [選取要延展的資料列]  對話方塊隨即開啟。  
  
     ![定義以日期為基礎的篩選述詞](../../sql-server/stretch-database/media/stretch-wizard-2a.png "定義以日期為基礎的篩選述詞")  
  
2.  在 [選取要延展的資料列]  對話方塊中，選取 [選擇資料列]  。  
  
3.  在 [名稱]  欄位中，提供篩選函數的名稱。  
  
4.  針對 **Where** 子句，選取資料表中的資料行、挑選一個運算子，並提供值。  
  
5.  按一下 [檢查]  以測試函數。 如果函數從資料表傳回結果 - 也就是有要移轉的資料列符合條件 - 測試會回報**成功**。  

> [!NOTE] 
> 顯示篩選查詢的文字方塊是唯讀的。 您無法編輯文字方塊中的查詢。
  
6.  按一下 [完成] 返回 [選取資料表]  頁面。  

篩選函數只有在您完成精靈時才會建立在 SQL Server 中。 在那之前，您可以回到 [選取資料表]  頁面，變更或重新命名篩選函數。

![定義篩選述詞之後的 [選取資料表] 頁面](../../sql-server/stretch-database/media/stretch-wizard-2b.png "定義篩選述詞之後的 [選取資料表] 頁面")

如果您想要使用不同類型的篩選函數來選取要移轉的資料列，請執行下列其中一項操作。  
  
-   結束精靈，然後執行 ALTER TABLE 陳述式來啟用資料表的延展功能以及指定篩選函數。 如需詳細資訊，請參閱 [為資料表啟用 Stretch Database](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md)。  
  
-   結束精靈之後，請執行 ALTER TABLE 陳述式來指定篩選函數。 如需必要的步驟，請參閱 [Add a filter function after running the Wizard](../../sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md#addafterwiz)(在執行精靈後新增篩選函數)。  
  
##  <a name="Configure"></a> 設定 Azure  
  
1.  使用 Microsoft 帳戶登入 Microsoft Azure。  
  
     ![登入 Azure - Stretch Database 精靈](../../sql-server/stretch-database/media/stretch-wizard-3.png "登入 Azure - Stretch Database 精靈")  
  
2.  選取要用於 Stretch Database 的現有 Azure 訂用帳戶。 

> [!NOTE] 
> 若要在資料庫上啟用延展，您必須具有您所使用之訂用帳戶的系統管理員權限。 Stretch Database 精靈只會顯示使用者具有系統管理員權限的訂用帳戶。
  
3.  選取要用於 Stretch Database 的 Azure 區域。
    -   如果您建立新的伺服器，該伺服器就會建立於此區域中。  
    -   如果您在所選區域中有現有的伺服器，精靈會在您選擇 [現有伺服器]  時列出它們。
  
     若要將延遲降至最低，請挑選您的 SQL Server 所在的 Azure 區域。 如需區域的詳細資訊，請參閱 [Azure 區域](https://azure.microsoft.com/regions/)。  
  
4.  指定您要使用現有的伺服器，或建立新的 Azure 伺服器。  
  
     如果您 SQL Server 上的 Active Directory 會與 Azure Active Directory 同盟，就可以選擇性地使用適用於 SQL Server 的同盟服務帳戶，來與遠端 Azure 伺服器通訊。 如需此選項需求的詳細資訊，請參閱 [ALTER DATABASE SET 選項 &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)。  
  
    -   **建立新的伺服器**  
  
        1.  為伺服器系統管理員建立登入和密碼。  
  
        2.  您可以選擇性地使用適用於 SQL Server 的同盟服務帳戶，來與遠端 Azure 伺服器通訊。  
  
         ![建立新的 Azure 伺服器 - Stretch Database 精靈](../../relational-databases/tables/media/stretch-wizard-4.png "建立新的 Azure 伺服器 - Stretch Database 精靈")  
  
    -   **現有的伺服器**  
  
        1.  選取現有的 Azure 伺服器。  
  
        2.  選取驗證方法。  
  
            -   如果您選取 [SQL Server 驗證]  ，請提供系統管理員登入與密碼。  
  
            -   選取 [Active Directory 整合式驗證]  ，使用適用於 SQL Server 的同盟服務帳戶，來與遠端 Azure 伺服器通訊。 如果選取的伺服器未與 Azure Active Directory 整合，則不會出現此選項。
  
         ![選取現有的 Azure 伺服器 - Stretch Database 精靈](../../sql-server/stretch-database/media/stretch-wizard-5.png "選取現有的 Azure 伺服器 - Stretch Database 精靈")  
  
##  <a name="Credentials"></a> 安全認證  
 您必須擁有資料庫主要金鑰，才能保護認證安全，Stretch Database 會使用這類認證來連接遠端資料庫。  
  
 如果資料庫主要金鑰已存在，請為其輸入密碼。  
  
 ![Stretch Database 精靈的 [安全認證] 頁面](../../sql-server/stretch-database/media/stretch-wizard-6b.PNG "Stretch Database 精靈的 [安全認證] 頁面")  
  
 如果資料庫沒有現有的主要金鑰，請輸入強式密碼來建立資料庫主要金鑰。  
  
 ![Stretch Database 精靈的 [安全認證] 頁面](../../relational-databases/tables/media/stretch-wizard-6.png "Stretch Database 精靈的 [安全認證] 頁面")  
  
 如需資料庫主要金鑰的詳細資訊，請參閱 [CREATE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-master-key-transact-sql.md) 和[建立資料庫主要金鑰](../../relational-databases/security/encryption/create-a-database-master-key.md)。 如需精靈所建立之認證的詳細資訊，請參閱 [CREATE DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)。  
  
##  <a name="Network"></a> 選取 IP 位址  
 使用子網路 IP 位址範圍 (建議)，或您 SQL Server 的公用 IP 位址，在 Azure 上建立防火牆規則，讓 SQL Server 可與遠端 Azure 伺服器通訊。  
  
 您在此頁面提供的一或多個 IP 位址會告訴 Azure 伺服器，允許 SQL Server 初始的傳入資料、查詢作業通過 Azure 防火牆。 精靈不會在 SQL Server 的防火牆設定中變更任何項目。  
  
 ![ 精靈的 [選取 IP 位址] 頁面](../../relational-databases/tables/media/stretch-wizard-7.png "Stretch Database 精靈的 [選取 IP 位址] 頁面")  
  
##  <a name="Summary"></a> 摘要  
 檢閱您輸入的值、在精靈中選取的選項，以及在 Azure 上估計的成本。 然後選取 [完成]  以啟用 Stretch。  
  
 ![Stretch Database 精靈的 [摘要] 頁面](../../sql-server/stretch-database/media/stretch-wizard-8.png "Stretch Database 精靈的 [摘要] 頁面")  
  
##  <a name="Results"></a> 結果  
 檢閱結果。  
  
 若要監視資料移轉的狀態，請參閱[監視和疑難排解資料移轉 &#40;Stretch Database&#41;](../../sql-server/stretch-database/monitor-and-troubleshoot-data-migration-stretch-database.md)。  
  
 ![Stretch Database 精靈的 [結果] 頁面](../../sql-server/stretch-database/media/stretch-wizard-9.PNG "Stretch Database 精靈的 [結果] 頁面")  
  
##  <a name="KnownIssues"></a> 疑難排解精靈  
 **Stretch Database 精靈失敗。**  
 如果尚未在伺服器層級啟用 Stretch Database，而您在執行精靈來啟用它時未具備系統管理員權限，則精靈會失敗。 請要求系統管理員，在本機伺服器執行個體上啟用 Stretch Database，然後再次執行精靈。 如需詳細資訊，請參閱＜ [必要條件：在伺服器上啟用 Stretch Database 的權限](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md#EnableTSQLServer)＞。  
  
## <a name="next-steps"></a>後續步驟  
 為其他資料表啟用 Stretch Database。 監視資料移轉以及管理已啟用 Stretch 的資料庫和資料表。  
  
-   [Enable Stretch Database for a table](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md) 以啟用額外資料表。  
  
-   [監視和疑難排解資料移轉 &#40;Stretch Database&#41;](../../sql-server/stretch-database/monitor-and-troubleshoot-data-migration-stretch-database.md) 以查看資料移轉狀態。  
  
-   [暫停和繼續資料移轉 &#40;Stretch Database&#41;](../../sql-server/stretch-database/pause-and-resume-data-migration-stretch-database.md)  
  
-   [管理 Stretch Database 並對其進行疑難排解](../../sql-server/stretch-database/manage-and-troubleshoot-stretch-database.md)  
  
-   [備份已啟用 Stretch 的資料庫](../../sql-server/stretch-database/backup-stretch-enabled-databases-stretch-database.md)  
  
-   [還原已啟用 Stretch 的資料庫](../../sql-server/stretch-database/restore-stretch-enabled-databases-stretch-database.md)  
  
## <a name="see-also"></a>另請參閱  
 [Enable Stretch Database for a database](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md)   
 [為資料表啟用 Stretch Database](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md)  
  
  
