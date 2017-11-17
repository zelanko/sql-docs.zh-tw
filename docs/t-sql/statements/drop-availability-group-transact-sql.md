---
title: "卸除可用性群組 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP_AVAILABILITY_GROUP_TSQL
- DROP AVAILABILITY GROUP
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], removing
- Availability Groups [SQL Server], Transact-SQL statements
- DROP AVAILABILITY GROUP statement
- Availability Groups [SQL Server], dropping
ms.assetid: c1600289-c990-454a-b279-dba0ebd5d63e
caps.latest.revision: 44
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c1cd1e16d7d25810d571f940aaf1dece825406c3
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="drop-availability-group-transact-sql"></a>DROP AVAILABILITY GROUP (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  移除指定的可用性群組以及其所有複本。 如果當您刪除可用性群組時，裝載其中一個可用性複本的伺服器執行個體離線，則在回到線上之後此伺服器執行個體將會卸除本機可用性複本。 卸除可用性群組也會刪除關聯的可用性群組接聽程式 (如果有的話)。  
  
> [!IMPORTANT]  
>  如果可能的話，只在連接主控主要複本的伺服器執行個體時移除可用性群組。 從主要複本卸除可用性群組時，就可以在舊的主要資料庫中進行變更 (沒有高可用性保護)。 從次要複本刪除可用性群組會讓主要複本的**RESTORING**狀態，以及變更不允許在資料庫上。  
  
 若要卸除可用性群組的替代方式的相關資訊，請參閱[移除可用性群組 &#40;SQL Server &#41;](../../database-engine/availability-groups/windows/remove-an-availability-group-sql-server.md).  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
DROP AVAILABILITY GROUP group_name   
[ ; ]  
```  
  
## <a name="arguments"></a>引數  
 *群組名稱*  
 指定要卸除的可用性群組名稱。  
  
## <a name="limitations-and-recommendations"></a>限制與建議  
  
-   執行**DROP AVAILABILITY GROUP**需要伺服器執行個體上啟用 Alwayson 可用性群組功能。 如需詳細資訊，請參閱[啟用和停用 AlwaysOn 可用性群組 &#40;SQL Server &#41;](../../database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md).  
  
-   **DROP AVAILABILITY GROUP**無法執行，因為交易內批次的一部分。 此外，運算式和變數也不支援。  
  
-   您可以從任何擁有可用性群組之正確安全性認證的 Windows Server 容錯移轉叢集 (WSFC) 節點中卸除可用性群組。 如此一來，當可用性群組沒有任何可用性複本存在時，就可以刪除此可用性群組。  
  
    > [!IMPORTANT]  
    >  避免在 Windows Server 容錯移轉叢集 (WSFC) 叢集沒有仲裁時卸除可用性群組。 如果您必須在叢集缺少仲裁時卸除可用性群組，儲存在叢集中的中繼資料可用性群組並不會移除。 在叢集重新取得仲裁之後，您將需要再次卸除可用性群組，以便從 WSFC 叢集中將它移除。  
  
-   次要複本上， **DROP AVAILABILITY GROUP**應該只用於只供緊急使用。 這是因為卸除可用性群組會讓可用性群組離線。 如果您從次要複本卸除可用性群組，就無法判斷主要複本是否**離線**狀態是因為遺失仲裁、 強制容錯移轉，而發生或**DROP AVAILABILITY GROUP**命令。 主要複本會轉換到**RESTORING**狀態，以防止可能的裂腦情況發生。 如需詳細資訊，請參閱 [How It Works: DROP AVAILABILITY GROUP Behaviors](http://blogs.msdn.com/b/psssql/archive/2012/06/13/how-it-works-drop-availability-group-behaviors.aspx) (運作方式：DROP AVAILABILITY GROUP 行為) (CSS SQL Server 工程師部落格)。  
  
## <a name="security"></a>安全性  
  
### <a name="permissions"></a>Permissions  
 需要**ALTER AVAILABILITY GROUP**可用性群組中，權限**CONTROL AVAILABILITY GROUP**權限， **ALTER ANY AVAILABILITY GROUP**權限，或**CONTROL SERVER**權限。 若要卸除可用性群組，您需要在本機伺服器執行個體所未裝載**CONTROL SERVER**權限或**控制項**該可用性群組的權限。  
  
## <a name="examples"></a>範例  
 下列範例會卸除 `AccountsAG` 可用性群組。  
  
```  
DROP AVAILABILITY GROUP AccountsAG;  
```  
  
##  <a name="RelatedContent"></a> 相關內容  
  
-   [How It Works: DROP AVAILABILITY GROUP Behaviors](http://blogs.msdn.com/b/psssql/archive/2012/06/13/how-it-works-drop-availability-group-behaviors.aspx) (運作方式：DROP AVAILABILITY GROUP 行為) (CSS SQL Server 工程師部落格)  
  
## <a name="see-also"></a>另請參閱  
 [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-availability-group-transact-sql.md)   
 [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-availability-group-transact-sql.md)   
 [移除可用性群組 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/remove-an-availability-group-sql-server.md)  
  
  

