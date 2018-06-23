---
title: master 資料庫 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- master database [SQL Server], about
- master database [SQL Server]
ms.assetid: 660e909f-61eb-406b-bbce-8864dd629ba0
caps.latest.revision: 46
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 88cbd58a75ff8b7ceaaf93843bb685cdcb8dc11b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36132676"
---
# <a name="master-database"></a>master 資料庫
  **master** 資料庫會記錄 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統的所有系統層級資訊。 這包括了整個執行個體範圍的中繼資料，例如登入帳戶、端點、連結的伺服器，以及系統組態設定。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中，系統物件不再儲存於 **master** 資料庫，而是儲存於 [Resource 資料庫](resource-database.md)。 **master** 資料庫也會記錄所有其他資料庫的存在與這些資料庫檔案的所在位置，並記錄 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的初始化資訊。 因此，如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] master **資料庫無法使用，** 也會無法啟動。  
  
## <a name="physical-properties-of-master"></a>master 的實體屬性  
 下表列出了 **master** 資料與記錄檔的初始組態值。 對於不同版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，這些檔案的大小稍有不同。  
  
|檔案|邏輯名稱|實體名稱|檔案成長|  
|----------|------------------|-------------------|-----------------|  
|主要資料|master|Master.mdf|以 10% 的比例自動成長，直到磁碟已滿。|  
|Log|mastlog|mastlog.ldf|以 10% 的比例自動成長，最大至 2 TB。|  
  
 如需如何移動 **master** 資料與記錄檔的資訊，請參閱 [移動系統資料庫](system-databases.md)。  
  
### <a name="database-options"></a>資料庫選項  
 下表列出了 **master** 資料庫中每個資料庫選項的預設值，以及是否可修改該選項。 若要檢視這些選項目前的設定，請參閱 [sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) 目錄檢視。  
  
|資料庫選項|預設值|可以修改|  
|---------------------|-------------------|---------------------|  
|ALLOW_SNAPSHOT_ISOLATION|ON|否|  
|ANSI_NULL_DEFAULT|OFF|是|  
|ANSI_NULLS|OFF|是|  
|ANSI_PADDING|OFF|是|  
|ANSI_WARNINGS|OFF|是|  
|ARITHABORT|OFF|是|  
|AUTO_CLOSE|OFF|否|  
|AUTO_CREATE_STATISTICS|ON|是|  
|AUTO_SHRINK|OFF|否|  
|AUTO_UPDATE_STATISTICS|ON|是|  
|AUTO_UPDATE_STATISTICS_ASYNC|OFF|是|  
|CHANGE_TRACKING|OFF|否|  
|CONCAT_NULL_YIELDS_NULL|OFF|是|  
|CURSOR_CLOSE_ON_COMMIT|OFF|是|  
|CURSOR_DEFAULT|GLOBAL|是|  
|資料庫可用性選項|ONLINE<br /><br /> MULTI_USER<br /><br /> READ_WRITE|否<br /><br /> 否<br /><br /> 否|  
|DATE_CORRELATION_OPTIMIZATION|OFF|是|  
|DB_CHAINING|ON|否|  
|ENCRYPTION|OFF|否|  
|NUMERIC_ROUNDABORT|OFF|是|  
|PAGE_VERIFY|CHECKSUM|是|  
|PARAMETERIZATION|SIMPLE|是|  
|QUOTED_IDENTIFIER|OFF|是|  
|READ_COMMITTED_SNAPSHOT|OFF|否|  
|RECOVERY|SIMPLE|是|  
|RECURSIVE_TRIGGERS|OFF|是|  
|Service Broker 選項|DISABLE_BROKER|否|  
|TRUSTWORTHY|OFF|是|  
  
 如需這些資料庫選項的描述，請參閱 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)。  
  
## <a name="restrictions"></a>限制  
 您不能在 **master** 資料庫上執行下列作業：  
  
-   加入檔案或檔案群組。  
  
-   變更定序。 預設定序是伺服器定序。  
  
-   變更資料庫擁有者。 **master** 是由 **sa**所擁有。  
  
-   建立全文檢索目錄或全文檢索索引。  
  
-   在資料庫中的系統資料表上建立觸發程序。  
  
-   卸除資料庫。  
  
-   從資料庫卸除 **guest** 使用者。  
  
-   啟用異動資料擷取。  
  
-   參與資料庫鏡像。  
  
-   移除主要檔案群組、主要資料檔或記錄檔。  
  
-   重新命名資料庫或主要檔案群組。  
  
-   將資料庫設定為 OFFLINE。  
  
-   將資料庫或主要檔案群組設定為 READ_ONLY。  
  
## <a name="recommendations"></a>建議  
 當您使用 **master** 資料庫時，請考慮下列建議：  
  
-   永遠保留 **master** 資料庫的最新備份。  
  
-   在執行下列作業後，立即備份 **master** 資料庫：  
  
    -   建立、修改或卸除任何資料庫  
  
    -   變更伺服器或資料庫組態值  
  
    -   修改或加入登入帳戶  
  
-   請勿在 **master**中建立使用者物件。 如果您這樣做，就必須更經常地備份 **master** 。  
  
-   請勿將 **master** 資料庫的 TRUSTWORTHY 選項設為 ON。  
  
## <a name="what-to-do-if-master-becomes-unusable"></a>如果 master 變得無法使用該怎麼辦  
 如果 **master** 資料庫變得無法使用，您可以使用下列任一方法將資料庫回復到可用狀態：  
  
-   從現行資料庫備份來還原 **master** 。  
  
     如果您可以啟動伺服器執行個體，應該就能夠從完整資料庫備份來還原 **master** 。 如需詳細資訊，請參閱 [還原 master 資料庫 &#40;Transact-SQL&#41;](../backup-restore/restore-the-master-database-transact-sql.md)。  
  
-   完全重建 **master** 。  
  
     如果 **master** 嚴重損壞，使您無法啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，則必須重建 **master**。 如需詳細資訊，請參閱 [重建系統資料庫](rebuild-system-databases.md)。  
  
    > [!IMPORTANT]  
    >  重建 **master** 將會重建所有的系統資料庫。  
  
## <a name="related-content"></a>相關內容  
 [重建系統資料庫](rebuild-system-databases.md)  
  
 [系統資料庫](system-databases.md)  
  
 [sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)  
  
 [sys.master_files &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-master-files-transact-sql)  
  
 [移動資料庫檔案](move-database-files.md)  
  
  
