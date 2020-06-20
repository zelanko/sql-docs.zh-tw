---
title: 啟用及設定 FILESTREAM | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.technology: filestream
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], enabling
ms.assetid: 78737e19-c65b-48d9-8fa9-aa6f1e1bce73
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 7312df919f6d182351e86ed41b5aed84fba3e646
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84955508"
---
# <a name="enable-and-configure-filestream"></a>啟用及設定 FILESTREAM
  在您開始使用 FILESTREAM 之前，必須先在 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]執行個體上啟用 FILESTREAM。 此主題描述如何使用 SQL Server 組態管理員來啟用 FILESTREAM。  
  
> [!NOTE]  
>  您無法針對在 64 位元作業系統上執行的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 32 位元版本啟用 FILESTREAM。  
  
##  <a name="enabling-filestream"></a><a name="enabling"></a> 啟用 FILESTREAM  
  
#### <a name="to-enable-and-change-filestream-settings"></a>若要啟用和變更 FILESTREAM 設定  
  
1.  指向 **[開始]** 功能表上的 **[所有程式]** ，然後依序指向 [ [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]] 和 **[組態工具]** ，再按一下 **[SQL Server 組態管理員]** 。  
  
2.  在服務的清單中，以滑鼠右鍵按一下 [SQL Server 服務]  ，然後按一下 [開啟]  。  
  
3.  在 [SQL Server 組態管理員]  嵌入式管理單元中，找出您想要啟用 FILESTREAM 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。  
  
4.  以滑鼠右鍵按一下該執行個體，然後按一下 [屬性]  。  
  
5.  在 [SQL Server 屬性]  對話方塊中，按一下 [FILESTREAM]  索引標籤。  
  
6.  選取 [啟用 FILESTREAM 的 Transact-SQL 存取]  核取方塊。  
  
7.  如果您想要從 Windows 讀取和寫入 FILESTREAM 資料，請按一下 [啟用 FILESTREAM 的檔案 I/O 資料流存取]  。 在 [Windows 共用名稱]  方塊中，輸入 Windows 共用的名稱。  
  
8.  如果遠端用戶端必須存取儲存在這個共用上的 FILESTREAM 資料，請選取 [允許遠端用戶端具有 FILESTREAM 資料的資料流存取權]  。  
  
9. 按一下 [套用]  。  
  
10. 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，按一下 **[新增查詢]** 顯示 [查詢編輯器]。  
  
11. 在 [查詢編輯器] 中，輸入下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 程式碼：  
  
    ```sql  
    EXEC sp_configure filestream_access_level, 2  
    RECONFIGURE  
    ```  
  
12. 按一下 **[執行]** 。  
  
13. 重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務。  
  

  
##  <a name="best-practices"></a><a name="best"></a>最佳做法  
  
###  <a name="physical-configuration-and-maintenance"></a><a name="config"></a>實體設定和維護  
 當您設定 FILESTREAM 儲存體磁碟區時，請考慮下列指導方針：  
  
-   在 FILESTREAM 電腦系統上關閉簡短檔案名稱。 簡短檔案名稱會花費更長的時間來建立。 若要停用簡短檔案名稱，請使用 Windows **fsutil** 公用程式。  
  
-   定期重組 FILESTREAM 電腦系統。  
  
-   使用 64-KB NTFS 叢集。 壓縮的磁碟區必須設定為 4-KB NTFS 叢集。  
  
-   停用 FILESTREAM 磁碟區上的索引，並設定 **disablelastaccess** 。若要設定 **disablelastaccess**，請使用 Windows **fsutil** 公用程式。  
  
-   在必要的情況下，停用 FILESTREAM 磁碟區的防毒掃描。 如果防毒掃描是必要的功能，請避免設定自動刪除違規檔案的原則。  
  
-   針對容錯和應用程式所需的效能設定並微調 RAID 層級。  
  
||||||  
|-|-|-|-|-|  
|RAID 層級|寫入效能|讀取效能|容錯|備註|  
|RAID 5|正常|正常|非常好|效能高於單一磁碟或 JBOD，而低於具有條狀配置的 RAID 0 或 RAID 5。|  
|RAID 0|非常好|非常好|None||  
|RAID 5 + 條狀配置|非常好|非常好|非常好|成本最高的選項。|  
  

  
###  <a name="physical-database-design"></a><a name="database"></a>實體資料庫設計  
 當您設計 FILESTREAM 資料庫時，請考慮下列指導方針：  
  
-   FILESTREAM 資料行必須伴隨對應的 `uniqueidentifier` ROWGUID 資料行。 這些種類的資料表也必須附帶唯一的索引。 一般而言，這個索引不是叢集索引。 如果資料庫商務邏輯需要叢集索引，您就必須確定儲存在索引中的值不是隨機的。 隨機值將會導致每次在資料表中加入或移除資料列時，重新排列索引。  
  
-   基於效能考量，FILESTREAM 檔案群組和容器應該位於作業系統、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 記錄、tempdb 或分頁檔以外的磁碟區上。  
  
-   FILESTREAM 無法直接支援空間管理和原則。 不過，您可以透過將每個 FILESTREAM 檔案群組指派至個別的磁碟區，並使用磁碟區的管理功能，以間接方式管理空間和套用原則。  
  
  
