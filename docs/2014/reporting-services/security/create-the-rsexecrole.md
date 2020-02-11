---
title: 建立 RSExecRole | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- RSExecRole
ms.assetid: 7ac17341-df7e-4401-870e-652caa2859c0
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 3a6bc5ecbd1c59a5dc03f9c28d36d2816e6a8d92
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66102024"
---
# <a name="create-the-rsexecrole"></a>建立 RSExecRole
  
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 會使用稱為 `RSExecRole` 之預先定義的資料庫角色，授與報表伺服器對於報表伺服器資料庫的權限。 
  `RSExecRole` 角色會自動與報表伺服器資料庫一起建立。 您絕對不能修改它或是將其他使用者指派給這個角色，這是一般的規則。 不過，當您將報表伺服器資料庫移至新的或不同[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../../includes/ssde-md.md)]的時，必須在 Master 和 MSDB 系統資料庫中重新建立該角色。  
  
 使用下列指示執行下列步驟：  
  
-   在 Master 系統資料庫中建立及提供 `RSExecRole`。  
  
-   在 MSDB 系統資料庫中建立及提供 `RSExecRole`。  
  
> [!NOTE]  
>  本主題的指示適用於不想要執行指令碼或撰寫 WMI 程式碼來提供報表伺服器資料庫的使用者。 如果您管理大型部署，而且平常都會移動資料庫，您應該撰寫指令碼，讓這些步驟自動化。 如需詳細資訊，請參閱 [存取 Reporting Services WMI 提供者](../tools/access-the-reporting-services-wmi-provider.md)。  
  
## <a name="before-you-start"></a>開始之前  
  
-   請備份加密金鑰，好讓您可以在移動資料庫之後還原這些金鑰。 這個步驟不會直接影響您建立及提供 `RSExecRole` 的能力，但是您必須擁有金鑰的備份，才能夠確認您的工作。 如需詳細資訊，請參閱 [備份與還原 Reporting Services 加密金鑰](../install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)。  
  
-   請確認您已經使用具有 `sysadmin` 執行個體上 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 權限的使用者帳戶登入。  
  
-   請確認在您打算使用的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體上已安裝及執行 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] Agent 服務。  
  
-   附加 reportservertempdb 和 reportserver 資料庫。 您不需要附加這些資料庫也可以建立實際角色，但是在您測試工作以前，必須要附加這些資料庫。  
  
 手動建立 `RSExecRole` 的指示是要用於移轉報表伺服器安裝的環境。 本主題不會說明類似備份及移動報表伺服器資料庫等重要工作，這些工作記載於 Database Engine 文件集內。  
  
## <a name="create-rsexecrole-in-master"></a>在 Master 資料庫中建立 RSExecRole  
 
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 會使用適用於 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent 服務的擴充預存程序來支援排程作業。 下列步驟說明如何將這些程序的 Execute 權限授與給 `RSExecRole` 角色。  
  
#### <a name="to-create-rsexecrole-in-the-master-system-database-using-management-studio"></a>使用 Management Studio 在 Master 系統資料庫中建立 RSExecRole  
  
1.  啟動[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]並連接到主控[!INCLUDE[ssDE](../../../includes/ssde-md.md)]報表伺服器資料庫的實例。  
  
2.  開啟 **[資料庫]**。  
  
3.  開啟 **[系統資料庫]**。  
  
4.  開啟 `Master`。  
  
5.  開啟 **[安全性]**。  
  
6.  開啟 **[角色]**。  
  
7.  以滑鼠右鍵按一下 **[資料庫角色]**，然後選取 **[新增資料庫角色]**。 [一般] 頁面隨即出現。  
  
8.  在 [**角色名稱**] `RSExecRole`中，輸入。  
  
9. 在 [**擁有**者] 中輸入**DBO**。  
  
10. 按一下 **[安全性實體]**。  
  
11. 按一下 **[搜尋]** 。 
  **[加入物件]** 對話方塊隨即出現。 預設會選取 **[特定物件]** 選項。  
  
12. 按一下 [確定]  。 
  **[選取物件]** 對話方塊隨即出現。  
  
13. 按一下 **[物件類型]**。  
  
14. 按一下 **[擴充預存程序]**。  
  
15. 按一下 [確定]  。  
  
16. 按一下 **[瀏覽]** 。  
  
17. 向下捲動擴充預存程序的清單，並選取以下項目：  
  
    1.  xp_sqlagent_enum_jobs  
  
    2.  xp_sqlagent_is_starting  
  
    3.  xp_sqlagent_notify  
  
18. 按一下 **[確定]**，再按一下 **[確定]** 。  
  
19. 在 **[Execute]** 資料列中，按一下 **[授與]** 資料行內的核取方塊，然後按一下 **[確定]**。  
  
20. 針對每個剩餘的預存程序重複此步驟。 
  `RSExecRole` 必須針對所有三個預存程序授與「執行」權限。  
  
 ![資料庫角色屬性頁面](../media/rsexecroledbproperties.gif "資料庫角色屬性頁面")  
  
## <a name="create-rsexecrole-in-msdb"></a>在 MSDB 資料庫中建立 RSExecRole  
 Reporting Services 會使用適用於 SQL Server Agent 服務的預存程序，並從系統資料表擷取作業資訊來支援排程作業。 下列步驟說明如何將這些程序的 Execute 權限及資料表的 Select 權限授與給 RSExecRole。  
  
#### <a name="to-create-rsexecrole-in-the-msdb-system-database"></a>在 MSDB 系統資料庫中建立 RSExecRole  
  
1.  重複類似的步驟來授與 MSDB 中預存程序和資料表的權限。 為了簡化步驟，您將會個別提供預存程序和資料表。  
  
2.  開啟 `MSDB`。  
  
3.  開啟 **[安全性]**。  
  
4.  開啟 **[角色]**。  
  
5.  以滑鼠右鍵按一下 **[資料庫角色]**，然後選取 **[新增資料庫角色]**。 [一般] 頁面隨即出現。  
  
6.  在 [角色名稱] `RSExecRole`中，輸入。  
  
7.  在 [擁有者] 中輸入**DBO**。  
  
8.  按一下 **[安全性實體]**。  
  
9. 按一下 [新增]  。 
  **[加入物件]** 對話方塊隨即出現。 預設會選取 **[指定物件]** 選項。  
  
10. 按一下 [確定]  。  
  
11. 按一下 **[物件類型]**。  
  
12. 按一下 **[預存程序]**。  
  
13. 按一下 [確定]  。  
  
14. 按一下 **[瀏覽]** 。  
  
15. 向下捲動項目的清單，並選取以下項目：  
  
    1.  sp_add_category  
  
    2.  sp_add_job  
  
    3.  sp_add_jobschedule  
  
    4.  sp_add_jobserver  
  
    5.  sp_add_jobstep  
  
    6.  sp_delete_job  
  
    7.  sp_help_category  
  
    8.  sp_help_job  
  
    9. sp_help_jobschedule  
  
    10. sp_verify_job_identifiers  
  
16. 按一下 **[確定]**，再按一下 **[確定]** 。  
  
17. 選取第一個預存程序：sp_add_category。  
  
18. 在 **[Execute]** 資料列中，按一下 **[授與]** 資料行內的核取方塊，然後按一下 **[確定]**。  
  
19. 針對每個剩餘的預存程序重複此步驟。 必須針對所有的十個預存程序為 RSExecRole 授與 Execute 權限。  
  
20. 在 [安全性實體] 索引標籤上，再次按一下 **[加入]** 。 
  **[加入物件]** 對話方塊隨即出現。 預設會選取 **[指定物件]** 選項。  
  
21. 按一下 [確定]  。  
  
22. 按一下 **[物件類型]**。  
  
23. 按一下 **[資料表]**。  
  
24. 按一下 [確定]  。  
  
25. 按一下 **[瀏覽]** 。  
  
26. 向下捲動項目的清單，並選取以下項目：  
  
    1.  syscategories  
  
    2.  sysjobs  
  
27. 按一下 **[確定]**，再按一下 **[確定]** 。  
  
28. 選取第一個資料表：syscategories。  
  
29. 在 **[Select]** 資料列中，按一下 **[授與]** 資料行內的核取方塊，然後按一下 **[確定]**。  
  
30. 針對 sysjobs 資料表重複此步驟。 必須針對這兩個資料表為 RSExecRole 授與 Select 權限。  
  
## <a name="move-the-report-server-database"></a>移動報表伺服器資料庫  
 在建立角色之後，您可以將報表伺服器資料庫移到新的 SQL Server 執行個體。 如需詳細資訊，請參閱 [將報表伺服器資料庫移至其他電腦 &#40;SSRS 原生模式&#41;](../report-server/moving-the-report-server-databases-to-another-computer-ssrs-native-mode.md)。  
  
 如果您要將 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 升級到 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]，您可以在移動資料庫之前或之後來升級。  
  
 當報表伺服器連接到報表伺服器資料庫時，報表伺服器資料庫將會自動升級到 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 。 升級此資料庫不需要任何特定步驟。  
  
## <a name="restore-encryption-keys-and-verify-your-work"></a>還原加密金鑰及確認工作  
 如果您已經附加報表伺服器資料庫，您現在應該能夠完成以下步驟來確認您的工作。  
  
#### <a name="to-verify-report-server-operability-after-a-database-move"></a>在移動資料庫之後確認報表伺服器是否可操作  
  
1.  啟動 Reporting Services 組態工具，並連接到報表伺服器。  
  
2.  按一下 **[資料庫]**。  
  
3.  按一下 **[變更資料庫]**。  
  
4.  按一下 **[選擇現有報表伺服器資料庫]**。  
  
5.  輸入 Database Engine 的伺服器名稱。 如果您將報表伺服器資料庫附加到具名執行個體，您應該使用以下格式鍵入此執行個體名稱：\<伺服器名稱>\\<執行個體名稱\>。  
  
6.  按一下 **[測試連接]** 。  
  
7.  按 [下一步]  。  
  
8.  在 [資料庫] 上，選取報表伺服器資料庫。  
  
9. 按 [下一步] ****，並且完成精靈。  
  
10. 按一下 **[加密金鑰]**。  
  
11. 按一下 [還原]****。  
  
12. 選取具有對稱金鑰之備份副本 (用來解密預存認證) 及報表伺服器資料庫中之連接資訊的強式檔案 (.snk)。  
  
13. 輸入密碼，並按一下 **[確定]**。  
  
14. 按一下 **[報表管理員 URL]**。  
  
15. 按一下此連結，開啟報表管理員。 您應該可從報表伺服器資料庫中看到報表伺服器項目。  
  
## <a name="see-also"></a>另請參閱  
 [將報表伺服器資料庫移至另一部電腦 &#40;SSRS 原生模式&#41;](../report-server/moving-the-report-server-databases-to-another-computer-ssrs-native-mode.md)   
 [Reporting Services 組態管理員 &#40;原生模式&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)   
 [建立原生模式報表伺服器資料庫 &#40;SSRS Configuration Manager&#41;](../install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md)   
 [備份與還原 Reporting Services 加密金鑰](../install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)  
  
  
