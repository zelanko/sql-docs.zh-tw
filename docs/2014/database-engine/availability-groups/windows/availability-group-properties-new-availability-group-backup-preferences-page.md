---
title: 可用性群組屬性：新增可用性群組（備份喜好設定頁面） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.availabilitygroupproperties.backuppreferences.f1
helpviewer_keywords:
- read-only routing
ms.assetid: 65fff22d-5963-4a8c-8b31-fe9ab247a03e
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8c60a2de7c36eef7f01338e2b8ea8abe29093490
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62790217"
---
# <a name="availability-group-properties-new-availability-group-backup-preferences-page"></a>可用性群組屬性：新增可用性群組 (備份喜好設定頁面)
  使用此對話方塊可以檢視和變更所選可用性群組的備份喜好設定。  
  
 **若要檢視可用性群組屬性**  
  
-   [檢視可用性群組屬性 &#40;SQL Server&#41;](view-availability-group-properties-sql-server.md)  
  
-   [使用 AlwaysOn 儀表板 &#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
## <a name="where-should-backups-occur"></a>執行備份的位置  
 **慣用次要**  
 指定應該在次要複本上進行備份，但是主要複本是唯一線上複本的情況例外。 在此情況下，應該在主要複本上進行備份。 這是預設選項。  
  
 **僅次要**  
 指定絕對不能在主要複本上執行備份。 如果主要複本是唯一的線上複本，不應該進行備份。  
  
 **主要**  
 指定備份一定要在主要複本上進行。 如果當您在次要複本上執行備份時，需要不支援的備份功能 (例如建立差異備份)，這個選項會很實用。  
  
 **任何複本**  
 指定當您選擇要執行備份的複本時，您希望備份作業忽略可用性複本的角色。 請注意，備份作業可能會評估其他因素，例如每個可用性複本的備份優先權，搭配其操作狀態和連接狀態。  
  
> [!IMPORTANT]  
>  不會強制執行備份喜好設定。 這個喜好設定的解譯取決於您在給定可用性群組之資料庫的備份作業中所編寫的邏輯 (如果有的話)。 如需詳細資訊，請參閱使用中[次要資料庫：次要複本上的備份（AlwaysOn 可用性群組）](active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md)。  
  
## <a name="replica-backup-priorities"></a>複本備份優先權  
 此方格顯示裝載可用性群組複本的每個伺服器執行個體的目前備份優先權。 您可以使用此方格變更一個或多個可用性複本的備份優先權。  
  
 **伺服器執行個體**  
 裝載可用性複本之 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體的名稱。  
  
 **備份優先權 (最低 = 1，最高 = 100)**  
 指定在這個複本上執行備份的優先權 (相對於相同可用性群組中的其他複本)。 這個值是 0 到 100 範圍之間的整數。 1 表示最低優先權，100 表示最高優先權。 如果 [備份優先權]  = 1，則只有當目前沒有更高優先權的可用性複本可用時，才會選擇此可用性複本來執行備份。  
  
 **排除複本**  
 決定是否絕對不要選擇這個可用性複本來執行備份。 例如，這對於您永遠不希望將備份容錯移轉到其中的遠端可用性複本十分有用。  
  
## <a name="see-also"></a>另請參閱  
 [作用中次要資料庫：次要複本上的備份（AlwaysOn 可用性群組）](active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md)   
 [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-availability-group-transact-sql)  
  
  
