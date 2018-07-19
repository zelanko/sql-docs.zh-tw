---
title: 在 Oracle 發行者端建立的物件 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Oracle publishing [SQL Server replication], objects created
ms.assetid: c58a124b-4da7-46e2-9292-af8ce9e6664b
caps.latest.revision: 32
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 671058db0556f58d6bd29b8960212b6e180862be
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37166901"
---
# <a name="objects-created-on-the-oracle-publisher"></a>在 Oracle 發行者端建立的物件
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 複寫會在 Oracle 發行者端安裝資料庫物件，以啟用變更追蹤和轉送 ([!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 不會在 Oracle 發行者端安裝任何二進位檔案)。 下表列出當「Oracle 發行者」在「 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 散發者」端上識別為「發行者」時，在該「Oracle 發行者」端上建立的物件。 提供的物件描述僅供參考之用。 不應對這些物件進行修改。  
  
|Object Name|物件類型|描述|  
|-----------------|-----------------|-----------------|  
|HREPL_ArticleNlog_V|Table|用於儲存已發行資料表進行變更時的資訊之變更追蹤資料表。 每個已發行資料表都會建立變更追蹤資料表。|  
|HREPL_Changes|Table|Xactset 作業內部用於決定等待被指派至交易集之變更數量的資料表。 如需此作業的詳細資訊，請參閱 [Oracle 發行者的效能微調](performance-tuning-for-oracle-publishers.md)。|  
|HREPL_Distributor|Table|用於維護與「Oracle 發行者」相關的「 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 散發者」資訊之散發者狀態資料表。|  
|HREPL_Event|Table|用於同步處理快照集和資料列計數要求的事件資料表。|  
|HREPL_Mutex|Table|用於確保「記錄讀取器代理程式」和資料庫作業未同時執行 Oracle 封裝程序 PopulatePollTable 的資料表。|  
|HREPL_Poll|Table|用於識別與已發行資料表數組變更相關之記錄資料表項目的資料表。|  
|HREPL_PublishedTables|Table|包含異動複寫中各發行項之項目的資料表。|  
|HREPL_Publisher|Table|用於維護「發行者」特定資訊的發行者狀態資料表。|  
|HREPL_SchemaFilter|Table|包含透過「新增發行集精靈」發行時未顯示之結構描述的資料表。|  
|HREPL_XactsetCreateTimes|Table|識別各交易集相關的建立時間之資料表。|  
|HREPL_XactsetJob|Table|含有 Xactset 作業目前參數設定的資料表。|  
|HREPL_Pollid|序列|用於產生輪詢 ID 的順序。|  
|HREPL_Seq|序列|用於排序變更命令的順序。|  
|HREPL_Stmt|序列|用於產生陳述式 ID 的順序。|  
|HREPL|封裝和封裝主體|在「發行者」端建立的「發行者」支援程式碼封裝。|  
|MSSQLSERVERDISTRIBUTOR|公用同義字|HREPL_Distributor 資料表的公用同義字。 如果將「散發者」設定為與「Oracle 發行者」搭配使用，並且此公用同義字已存在於資料庫中，則系統將會卸除並重新建立此公用同義字。<br /><br /> 使用 [CASCADE] 選項卸除公用同義字和設定的 Oracle 複寫使用者，將會從「Oracle 發行者」端移除所有複寫物件。|  
|HREPL_Len_I_J_K|函數|在 Oracle 發行封裝程式碼之外定義的函數，可用於查詢 LONG 資料行的長度 (為具有已發行 LONG 資料行的資料表產生參數化命令時使用)。 系統會為每個具有 LONG 資料行的已發行資料表產生函數。|  
|HREPL_DropPublisher|程序|在 Oracle 發行封裝程式碼之外定義的程序，可用於卸除「Oracle 發行者」。|  
|HREPL_ExecuteCommand|程序|在 Oracle 發行封裝程式碼之外定義的程序，可用於在「發行者」端執行命令。|  
|HREPL_ArticleN_Trigger_Row|觸發程序|為每個已發行資料表產生的觸發程序，用來追蹤資料列變更。|  
|HREPL_ArticleN_Trigger_Stmt|觸發程序|為每個已發行資料表產生的觸發程序，用來追蹤陳述式層級變更。|  
|HREPL_Article_I_J|檢視|為每個已發行資料表建立的檢視，用於查詢已發行的資料表。|  
|HREPL_Log_I_J_K|檢視|為每個已發行資料表建立的檢視，用於查詢變更追蹤資料表。|  
  
## <a name="see-also"></a>另請參閱  
 [設定 Oracle 發行者](configure-an-oracle-publisher.md)   
 [Oracle 發行相關術語字彙](glossary-of-terms-for-oracle-publishing.md)   
 [Oracle 發行概觀](oracle-publishing-overview.md)  
  
  
