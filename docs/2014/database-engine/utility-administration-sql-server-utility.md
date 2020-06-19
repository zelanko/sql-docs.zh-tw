---
title: 公用程式管理（SQL Server 公用程式） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: 3e5a00c3-8905-40f0-9ddc-d924df9c2f0d
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: fca4ea655ffdcf8471d1340016d16f2c5b9c352a
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84927665"
---
# <a name="utility-administration-sql-server-utility"></a>公用程式管理 (SQL Server 公用程式)
  您可以使用 [公用程式管理] 索引標籤來管理 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 公用程式的原則、安全性和資料倉儲設定。 如需 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 公用程式概念的詳細資訊，請參閱 [SQL Server 公用程式的功能與工作](../relational-databases/manage/sql-server-utility-features-and-tasks.md)。  
  
## <a name="ui-element-list"></a>UI 元素清單  
 原則索引標籤 - 使用 [原則] 索引標籤來檢視或指定全域監視原則。  
  
 設定全域資料層應用程式監視原則。 若要展開這個選項的值清單，請按一下原則名稱旁的箭頭，或是按一下原則標題。  
 應用程式何時用完處理器容量？ 若要變更這個原則，請使用原則描述右邊的控制項，然後按一下 **[套用]**。 您也可以使用顯示畫面底部的按鈕來還原預設值或捨棄變更。  
  
-   處理器使用量的預設最大值為 70%。  
  
-   處理器使用量的預設最小值為 0%。  
  
 應用程式何時用完檔案空間？ 若要變更資料檔或記錄檔空間使用量的原則，請使用原則描述右邊的控制項，然後按一下 [套用] ****。 您也可以使用顯示畫面底部的按鈕來還原預設值或捨棄變更。  
  
-   檔案空間使用量的預設最大值為 70%。  
  
-   檔案空間使用量的預設最小值為 0%。  
  
 設定 SQL Server Managed 執行個體的全域應用程式監視原則。 若要展開這個選項的值清單，請按一下原則名稱旁的箭頭，或是按一下原則標題。  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的 Managed 執行個體何時用完處理器容量？ 若要變更這個原則，請使用原則描述右邊的控制項，然後按一下 **[套用]**。 您也可以使用顯示畫面底部的按鈕來還原預設值或捨棄變更。  
  
-   執行個體處理器使用量的預設最大值為 70%。  
  
-   執行個體處理器使用量的預設最小值為 0%。  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 電腦的 Managed 執行個體何時用完處理器容量？ 若要變更這個原則，請使用原則描述右邊的控制項，然後按一下 **[套用]**。 您也可以使用顯示畫面底部的按鈕來還原預設值或捨棄變更。  
  
-   電腦處理器使用量的預設最大值為 70%。  
  
-   電腦處理器使用量的預設最小值為 0%。  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的 Managed 執行個體何時用完檔案空間？ 若要變更資料檔或記錄檔空間使用量的原則，請使用原則描述右邊的控制項，然後按一下 **[套用]**。 您也可以使用顯示畫面底部的按鈕來還原預設值或捨棄變更。  
  
-   檔案空間使用量的預設最大值為 70%。  
  
-   檔案空間使用量的預設最小值為 0%。  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 電腦的 Managed 執行個體何時用完存放磁碟區空間？ 若要變更這個原則，請使用原則描述右邊的控制項，然後按一下 **[套用]**。 您也可以使用顯示畫面底部的按鈕來還原預設值或捨棄變更。  
  
-   電腦磁碟區空間使用量的預設最大值為 70%。  
  
-   電腦磁碟區空間使用量的預設最小值為 0%。  
  
 從高動態的資源中減少原則違規雜訊。 若要展開這項功能的控制項，請按一下顯示畫面右邊的向下箭頭。  
 如需詳細資訊，請參閱[降低 CPU 使用量原則中的雜訊 &#40;SQL Server 公用程式&#41;](../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)  
  
## <a name="ui-element-list"></a>UI 元素清單  
 安全性索引標籤 - 顯示有權從 UCP 管理或讀取的登入名稱。  
  
 從 UCP 選取將會加入至公用程式讀取者角色的登入。  
 公用程式讀取者權限可讓使用者帳戶：  
  
-   連接到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 公用程式。  
  
-   請參閱 SSMS 中公用程式總管內的所有視點。  
  
-   請參閱 SSMS 中公用程式總管內 [公用程式管理] 節點上的設定。  
  
 公用程式管理員可以將 SQL Server 執行個體註冊到 SQL Server 公用程式，並從 SQL Server 公用程式中移除 SQL Server 執行個體，也可以修改 Managed 執行個體的原則及修改 UCP 上的管理設定。  
  
 若要成為公用程式管理員，您必須擁有 SQL Server 執行個體的系統管理員 (sysadmin) 權限。 若要加入或變更 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] UCP 的使用者帳戶，請在 SSMS 中使用物件總管，將使用者加入至 SQL Server UCP 執行個體的伺服器登入。 如需詳細資訊，請參閱 [sp_addlogin &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addlogin-transact-sql)。  
  
## <a name="ui-element-list"></a>UI 元素清單  
 資料倉儲索引標籤 - 顯示公用程式管理資料倉儲的組態詳細資料。  
  
 資料保留  
 指定針對 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]Managed 執行個體所收集之使用量資訊的資料保留週期。 預設期間為 1 年。 最小值是 1 個月。 最長的支援期間為 2 年。  
  
 公用程式資料倉儲組態資訊  
 這一版的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]無法設定下列組態設定：  
  
-   UMDW 名稱： Sysutility_mdw_ \<GUID> _DATA。  
  
-   收集組上傳頻率：每隔 15 分鐘。  
  
 UMDW 目錄是可設定的： \<System drive> ： \Program Files\Microsoft SQL Server \ MSSQL10_50。 <UCP_Name> \mssql\data \\ ，其中 \<System drive> 通常是 C：\硬碟磁碟機. 記錄檔（UMDW_ \<GUID> _LOG）位於相同的目錄中。  
  
> [!NOTE]  
>  可以使用卸離/附加或 ALTER DATABASE 來變更 UMDW (sysutility_mdw) 檔案的位置。 我們建議使用 ALTER DATABASE。 如需詳細資訊，請參閱 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)。  
  
 回到原廠的預設值  
 若要將此索引標籤上的設定重設為預設值，請按一下 [還原預設值]**** 按鈕，然後按一下 [套用]****。  
  
## <a name="see-also"></a>另請參閱  
 [公用程式儀表板 &#40;SQL Server 公用程式&#41;](../../2014/database-engine/utility-dashboard-sql-server-utility.md)   
 [部署的資料層應用程式詳細資料 &#40;SQL Server 公用程式&#41;](../../2014/database-engine/deployed-data-tier-application-details-sql-server-utility.md)   
 [受管理的執行個體詳細資料 &#40;SQL Server 公用程式&#41;](../../2014/database-engine/managed-instance-details-sql-server-utility.md)   
 [監視 SQL Server 公用程式中的 SQL Server 執行個體](../relational-databases/manage/monitor-instances-of-sql-server-in-the-sql-server-utility.md)  
  
  
