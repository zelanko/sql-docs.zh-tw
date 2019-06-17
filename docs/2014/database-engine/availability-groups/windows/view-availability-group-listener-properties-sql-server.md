---
title: 檢視可用性群組接聽程式屬性 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.availabilitygrouplistenerproperties.general.f1
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
ms.assetid: aca0d016-3228-40b8-bdc3-285ed6d9b280
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: bdec432699b7d0a6152509ec6a53ddf452376d5c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62788024"
---
# <a name="view-availability-group-listener-properties-sql-server"></a>檢視可用性群組接聽程式屬性 (SQL Server)
  此主題描述如何使用 *中的* 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 來檢視 AlwaysOn [!INCLUDE[tsql](../../../includes/tsql-md.md)] 「可用性群組接聽程式」 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)](Availability Group Listener) 的屬性。  
  
-   **若要檢視接聽程式屬性，可使用下列項目：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 **若要檢視接聽程式屬性**  
  
1.  在 [物件總管] 中，連接到裝載您想要檢視其接聽程式之可用性群組的任何可用性複本的伺服器執行個體。 按一下伺服器名稱展開伺服器樹狀目錄。  
  
2.  依序展開 **[AlwaysOn 高可用性]** 節點和 **[可用性群組]** 節點。  
  
3.  展開可用性群組的節點，然後展開 **[可用性群組接聽程式]** 節點。  
  
4.  以滑鼠右鍵按一下您想要檢視的接聽程式，然後選取 [屬性]  命令。  
  
5.  這樣就會開啟 **[可用性群組接聽項屬性]** 對話方塊。 如需詳細資訊，請參閱本主題稍後的 [可用性群組接聽程式屬性 (對話方塊)](#AgListenerPropertiesDialog)。  
  
###  <a name="AgListenerPropertiesDialog"></a> 可用性群組接聽程式屬性 (對話方塊)  
 **接聽程式 DNS 名稱**  
 可用性群組接聽程式的網路名稱。  
  
 **通訊埠**  
 此接聽程式所使用的 TCP 通訊埠。  
  
> [!NOTE]  
>  如果您連接到主要複本，就可以使用此欄位來修改接聽程式的通訊埠編號。 這項作業需要可用性群組的 ALTER AVAILABILITY GROUP 權限、CONTROL AVAILABILITY GROUP 權限、ALTER ANY AVAILABILITY GROUP 權限或 CONTROL SERVER 權限。  
  
 **網路模式**  
 指出接聽程式所使用的 TCP 通訊協定，其中一個：  
  
 **DHCP**  
 接聽程式會使用執行動態主機設定通訊協定 (DHCP) 之伺服器所指派的動態 IP 位址。  
  
 **靜態 IP**  
 接聽程式會使用一個或多個靜態 IP 位址。 若要存取不同的子網路，可用性群組接聽程式必須使用靜態 IP 位址。  
  
 此方格會顯示接聽程式所接聽的每個子網路，以及與該子網路相關聯的 IP 位址。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 **若要檢視接聽程式屬性**  
  
 若要監視可用性群組接聽程式，請使用下列檢視：  
  
 [sys.availability_group_listener_ip_addresses](/sql/relational-databases/system-catalog-views/sys-availability-group-listener-ip-addresses-transact-sql)  
 針對目前上線供可用性群組接聽程式使用的每個符合標準虛擬 IP 位址傳回一個資料列。  
  
 **資料行名稱** ：listener_id、ip_address、ip_subnet_mask、is_dhcp、network_subnet_ip、network_subnet_prefix_length、network_subnet_ipv4_mask、state、state_desc  
  
 [sys.availability_group_listeners](/sql/relational-databases/system-catalog-views/sys-availability-group-listeners-transact-sql)  
 若為給定的可用性群組，傳回零個資料列，表示沒有網路名稱與可用性群組相關聯，或針對 WSFC 叢集中的每個可用性群組接聽程式組態傳回一個資料列。  
  
 **資料行名稱** ：group_id、listener_id、dns_name、port、is_conformant、ip_configuration_string_from_cluster  
  
 [sys.dm_tcp_listener_states](/sql/relational-databases/system-dynamic-management-views/sys-dm-tcp-listener-states-transact-sql)  
 針對每個 TCP 接聽程式傳回一個包含動態狀態資訊的資料列。  
  
 **資料行名稱** ：listener_id、ip_address、is_ipv4、port、type、type_desc、state、state_desc、start_time  
  
> [!NOTE]  
>  如需使用 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 監視 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 環境的詳細資訊，請參閱 [監視可用性群組 &#40;Transact-SQL&#41;](monitor-availability-groups-transact-sql.md)(Availability Group Listener) 的屬性。  
  
##  <a name="RelatedTasks"></a> 相關工作  
  
-   [建立或設定可用性群組接聽程式 &#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md)  
  
-   [移除可用性群組接聽程式 &#40;SQL Server&#41;](remove-an-availability-group-listener-sql-server.md)  
  
## <a name="see-also"></a>另請參閱  
 [AlwaysOn 可用性群組概觀&#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [可用性群組接聽程式、用戶端連接性及應用程式容錯移轉 &#40;SQL Server&#41;](../../listeners-client-connectivity-application-failover.md)   
 [監視可用性群組 &#40;Transact-SQL&#41;](monitor-availability-groups-transact-sql.md)  
  
  
