---
title: SQL Server Integration Services (SSIS) Scale Out 高可用性支援 | Microsoft Docs
description: 本文描述如何設定 SSIS Scale Out 的高可用性
ms.custom: performance
ms.date: 05/23/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
author: haoqian
ms.author: haoqian
manager: craigg
ms.openlocfilehash: 24768e1b230631009d94a1c449f08164157ed481
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/16/2019
ms.locfileid: "65718423"
---
# <a name="scale-out-support-for-high-availability"></a>高可用性的 Scale Out 支援

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



在 SSIS Scale Out 中，Scale Out Worker 端高可用性的提供是透過執行含多個 Scale Out Worker 的套件。

使用 [SSIS 目錄的 AlwaysOn](../catalog/ssis-catalog.md#always-on-for-ssis-catalog-ssisdb) 和 Windows 容錯移轉叢集可在 Scale Out Master 端達到高可用性。 在此解決方案中，多個 Scale Out Master 執行個體裝載於 Windows 容錯移轉叢集中。 關閉主要節點上的 Scale Out Master 服務或 SSISDB 時，次要節點上的服務或 SSISDB 會繼續接受使用者要求，並與 Scale Out Worker 通訊。

或者，使用 SQL Server 容錯移轉叢集執行個體，即可在 Scale Out Master 端達到高可用性。 請參閱 [Scale Out 透過 SQL Server 容錯移轉叢集執行個體支援高可用性](scale-out-failover-cluster-instance.md)。

若要使用 AlwaysOn for SSIS 目錄在 Scale Out Master 端設定高可用性，請執行下列動作：

## <a name="1-prerequisites"></a>1.Prerequisites
設定 Windows 容錯移轉叢集。 如需相關指示，請參閱[安裝適用於 Windows Server 2012 的容錯移轉叢集功能和工具](https://blogs.msdn.com/b/clustering/archive/2012/04/06/10291601.aspx)部落格文章。 在所有叢集節點上安裝功能和工具。

## <a name="2-install-scale-out-master-on-the-primary-node"></a>2.在主要節點上安裝 Scale Out Master
在 Scale Out Master 的主要節點上，安裝 SQL Server Database Engine Services、Integration Services 和 Scale Out Master。 

在安裝期間，執行下列動作：

### <a name="21-set-the-account-running-scale-out-master-service-to-a-domain-account"></a>2.1 將執行 Scale Out Master 服務的帳戶設定為網域帳戶
此帳戶未來必須可以存取 Windows 容錯移轉叢集的次要節點上的 SSISDB。 因為 Scale Out Master 服務和 SSISDB 可以個別容錯移轉，所以在容錯移轉之後可以不在相同的節點上。

![HA 伺服器設定](media/ha-server-config.PNG)

### <a name="22-include-the-dns-host-name-for-the-scale-out-master-service-in-the-cns-of-the-scale-out-master-certificate"></a>2.2 在 Scale Out Master 憑證的 CN 中包含 Scale Out Master 服務的 DNS 主機名稱

此主機名稱是 Scale Out Master 端點，這會建立為容錯移轉叢集中的泛型服務叢集，在 (請參閱步驟 7)。   (請務必提供 DNS 主機名稱而非伺服器名稱。)

![HA 主要設定](media/ha-master-config.PNG)

## <a name="3-install-scale-out-master-on-the-secondary-node"></a>3.在次要節點上安裝 Scale Out Master
在 Scale Out Master 的次要節點上，安裝 SQL Server Database Engine Services、Integration Services 和 Scale Out Master。 

使用與主要節點上所使用的相同 Scale Out Master 憑證。 使用私密金鑰來匯出主要節點上的 Scale Out Master SSL 憑證，並將它安裝至次要節點上本機電腦的根憑證存放區。 在次要節點上安裝 Scale Out Master 時選取此憑證。

![HA 主要設定 2](media/ha-master-config2.PNG)

> [!NOTE]
> 您可以對其他次要節點上的 Scale Out Master 重複這些作業，來設定多個備份 Scale Out Master。

## <a name="4-set-up-and-configure-ssisdb-support-for-always-on"></a>4.安裝和設定適用於 AlwaysOn 的 SSIS 支援

遵循 [AlwaysOn for SSIS 目錄 (SSISDB)](../catalog/ssis-catalog.md#always-on-for-ssis-catalog-ssisdb) 中安裝和設定 AlwaysOn for SSISDB 的指示。

此外，您還需要建立在其中新增 SSISDB 之可用性群組的可用性群組接聽程式。 請參閱[建立或設定可用性群組接聽程式](../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)。

## <a name="5-update-the-scale-out-master-service-configuration-file"></a>5.更新 Scale Out Master 服務設定檔
更新主要和次要節點上的 Scale Out Master 服務設定檔 `\<drive\>:\Program Files\Microsoft SQL Server\140\DTS\Binn\MasterSettings.config`。 將 **SqlServerName** 更新為 [可用性群組接聽程式 DNS 名稱],[連接埠]。

## <a name="6-enable-package-execution-logging"></a>6.啟用套件執行記錄

SSISDB 中的記錄是透過自動產生其密碼來登入 **##MS_SSISLogDBWorkerAgentLogin##** 所完成。 若要讓記錄適用於所有 SSISDB 複本，請執行下列動作

### <a name="61-change-the-password-of-msssislogdbworkeragentlogin-on-the-primary-sql-server"></a>6.1 變更主要 SQL Server 上 **##MS_SSISLogDBWorkerAgentLogin##** 的密碼

### <a name="62-add-the-login-to-the-secondary-sql-server"></a>6.2 新增次要 SQL Server 的登入

### <a name="63-update-the-connection-string-used-for-logging"></a>6.3 更新用於記錄的連接字串。
呼叫含下列參數值的預存程序 `[catalog].[update_logdb_info]`：

-   `@server_name = '[Availability Group Listener DNS name],[Port]'`

-   `@connection_string = 'Data Source=[Availability Group Listener DNS name],[Port];Initial Catalog=SSISDB;User Id=##MS_SSISLogDBWorkerAgentLogin##;Password=[Password]];'`

## <a name="7-configure-the-scale-out-master-service-role-of-the-windows-server-failover-cluster"></a>7.設定 Windows 伺服器容錯移轉叢集的 Scale Out Master 服務角色

1.  在容錯移轉叢集管理員中，連線至 Scale Out 的叢集。選取叢集。 選取功能表中的 [動作]，然後選取 [設定角色]。

2.  在 [高可用性精靈] 對話方塊中，選取 [選取角色] 頁面上的 [泛型服務]。 在 [選取服務] 頁面上，選取 [SQL Server Integration Services Scale Out Master 14.0]。

3.  在 [用戶端存取點] 頁面上，輸入 Scale Out Master 服務的 DNS 主機名稱。

    ![HA 精靈 1](media/ha-wizard1.PNG)

4.  完成精靈。

在 Azure 虛擬機器中，此設定步驟需要額外的步驟。 這些概念和步驟的完整說明不在本文範圍內。

1.  您必須設定 Azure 網域。 Windows Server 容錯移轉叢集需要叢集中之所有電腦皆為相同網域中的成員。 如需詳細資訊，請參閱[使用 Azure 入口網站啟用 Azure Active Directory Domain Services](https://docs.microsoft.com/azure/active-directory-domain-services/active-directory-ds-getting-started)。

2. 您必須設定 Azure Load Balancer。 這是可用性群組接聽程式的需求。 如需詳細資訊，請參閱[教學課程：在 Azure 入口網站中使用基本負載平衡器，將內部流量負載平衡到 VM](https://docs.microsoft.com/azure/load-balancer/tutorial-load-balancer-basic-internal-portal)。

## <a name="8-update-the-scale-out-master-address-in-ssisdb"></a>8.更新 SSISDB 中的 Scale Out Master 位址

在主要 SQL Server 上，搭配執行預存程序 `[catalog].[update_master_address]` 與參數值 `@MasterAddress = N'https://[Scale Out Master service DNS host name]:[Master Port]'`。 

## <a name="9-add-the-scale-out-workers"></a>9.新增 Scale Out Worker

現在，您可以透過 [Integration Services Scale Out Manager](integration-services-ssis-scale-out-manager.md) 的協助來新增 Scale Out Worker。 在連線頁面上輸入 `[SQL Server Availability Group Listener DNS name],[Port]`。

## <a name="upgrade-scale-out-in-high-availability-environment"></a>在高可用性環境中升級 Scale Out
若要在高可用性環境中升級 Scale Out，請遵循 [Always On for SSIS 目錄的升級步驟](../catalog/ssis-catalog.md#Upgrade)，並升級每部機器上的 Scale Out 主機和 Scale Out 背景工作，然後使用新版的 Scale Out 主機服務重新建立上面步驟 7 中的 Windows Server 容錯移轉叢集角色。

## <a name="next-steps"></a>後續步驟
如需詳細資訊，請參閱下列文章：
-   [Integration Services (SSIS) Scale Out Master](integration-services-ssis-scale-out-master.md)
-   [Integration Services (SSIS) Scale Out Worker](integration-services-ssis-scale-out-worker.md)
