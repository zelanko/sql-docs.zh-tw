---
title: "SQL Server 屬性 （啟動參數 索引標籤） |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: configuration-manager
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 16942624-5374-446c-8de4-ee6ed34d6e94
caps.latest.revision: "10"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 15243df46fad807a3078c9dfcd2c9043670ab05f
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="sql-server-properties-startup-parameters-tab"></a>SQL Server 屬性 (啟動參數索引標籤)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]使用此對話方塊來新增或移除的啟動參數， [!INCLUDE[ssDE](../../includes/ssde-md.md)]。 啟動參數可能會對 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 效能產生很大的影響。 加入或變更啟動參數之前，請先參閱《 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》中的＜使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務啟動選項＞主題。  
  
## <a name="options"></a>選項。  
 **指定啟動參數**  
 若要加入參數，請輸入參數，然後按一下 [加入]。  
  
 若要修改其中一個必要參數，請在 **[現有參數]** 方塊中選取參數、在 **[指定啟動參數]** 方塊中變更其值，然後按一下 **[更新]**。  
  
 **[現有參數]**  
 若要移除參數，請選取參數，然後按一下 [移除]。  
  
## <a name="parameter-format"></a>參數格式  
 請勿在參數之間輸入分隔符號。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員會自動加入分隔符號。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員會強制執行下列參數需求。  
  
-   修剪任何啟動參數中的開頭和尾端空白。  
  
-   所有啟動參數的開頭都是 - (虛線) 而第二個值是字母。  
  
## <a name="required-parameters"></a>必要參數  
 下列參數為必要參數。 您可以變更但無法移除這些參數。  
  
-   -d 是 **master.mdf** 檔案 (master 資料庫資料檔) 的路徑。  
  
-   -l 是 **master.ldf** 檔案 (master 資料庫記錄檔) 的路徑。  
  
-   -e 是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔的路徑。  
  
> [!CAUTION]  
>  如果檔案路徑不正確， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可能無法啟動。  
  
 如需有關如何移動 master 資料庫的詳細資訊，請參閱《 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》中的＜移動系統資料庫＞主題。  
  
## <a name="optional-parameters"></a>選擇性參數  
 《 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》中的＜使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務啟動選項＞主題描述了所有支援的啟動參數。 啟動參數 -T*trace#* 表示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體應該使用作用中的指定追蹤旗標 (*trace#*) 來啟動。 追蹤旗標用來啟動具有非標準行為的伺服器。 如需追蹤旗標的詳細資訊，請參閱《[!INCLUDE[tsql](../../includes/tsql-md.md)]線上叢書》中的＜追蹤旗標 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] )＞主題。  
  
> [!CAUTION]  
>  您可能會在網際網路上看到其他未記載的啟動參數和追蹤旗標描述。 未記載的啟動參數和追蹤旗標是用來處理不常見的問題或強制執行測試所需的特定條件。 使用未記載的啟動參數可能會產生非預期的結果。 除非 Microsoft 客戶支援服務建議使用未記載的參數，否則請勿使用這些參數。  
  
 下列清單描述的是一些常見的選擇性參數。  
  
|參數|簡短描述|  
|---------------|-----------------------|  
|-M|在單一使用者模式中啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。|  
|-T1204|傳回參與死結之鎖定的資源和類型，以及目前受影響的命令。|  
|-T1224|停用以鎖定個數為基礎的鎖定擴大。|  
|-T3608|防止 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 自動啟動並復原任何資料庫，但 master 資料庫除外。|  
|-T7806|在 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]上啟用專用管理員連接 (DAC)。|  
  
> [!CAUTION]  
>  某些選擇性參數可能會變更伺服器行為，而且可能會影響效能。  
  
## <a name="permissions"></a>Permissions  
 只有能夠在登錄中變更相關項目的使用者才能使用這個頁面， 包括下列使用者。  
  
-   本機 Administrators 群組的成員。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]所使用的網域帳戶 (如果 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 設定為使用網域帳戶來執行的話)。  
  
## <a name="books-online-references"></a>線上叢書參考  
 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 啟動參數的其他資訊，請參閱《[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》中的＜如何：設定伺服器啟動選項 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員)＞。  
  
  
