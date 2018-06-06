---
title: SQL Server Integration Services (SSIS) Scale Out 高可用性支援 | Microsoft Docs
ms.description: This article describes how to configure SSIS Scale Out for high availability
ms.custom: ''
ms.date: 12/19/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: scale-out
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
caps.latest.revision: 1
author: haoqian
ms.author: haoqian
manager: craigg
ms.openlocfilehash: 8cd79327b3733de9f7463f1d5f9d8f924b58a46b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="scale-out-support-for-high-availability"></a>高可用性的 Scale Out 支援

在 SSIS Scale Out 中，Scale Out Worker 端高可用性的提供是透過執行含多個 Scale Out Worker 的套件。

使用 [SSIS 目錄的 AlwaysOn](../catalog/ssis-catalog.md#always-on-for-ssis-catalog-ssisdb) 和 Windows 容錯移轉叢集可在 Scale Out Master 端達到高可用性。 在此解決方案中，多個 Scale Out Master 執行個體裝載於 Windows 容錯移轉叢集中。 關閉主要節點上的 Scale Out Master 服務或 SSISDB 時，次要節點上的服務或 SSISDB 會繼續接受使用者要求，並與 Scale Out Worker 通訊。

或者，使用 SQL Server 容錯移轉叢集執行個體，即可在 Scale Out Master 端達到高可用性。 請參閱 [Scale Out 透過 SQL Server 容錯移轉叢集執行個體支援高可用性](scale-out-failover-cluster-instance.md)。

若要使用 AlwaysOn for SSIS 目錄在 Scale Out Master 端設定高可用性，請執行下列動作：

## <a name="1-prerequisites"></a>1.Prerequisites
設定 Windows 容錯移轉叢集。 如需相關指示，請參閱[安裝適用於 Windows Server 2012 的容錯移轉叢集功能和工具](http://blogs.msdn.com/b/clustering/archive/2012/04/06/10291601.aspx)部落格文章。 在所有叢集節點上安裝功能和工具。

## <a name="2-install-scale-out-master-on-the-primary-node"></a>2.在主要節點上安裝 Scale Out Master
在 Scale Out Master 的主要節點上，安裝 SQL Server Database Engine Services、Integration Services 和 Scale Out Master。 

在安裝期間，執行下列動作：

### <a name="21-set-the-account-running-scale-out-master-service-to-a-domain-account"></a>2.1 將執行 Scale Out Master 服務的帳戶設定為網域帳戶
此帳戶未來必須可以存取 Windows 容錯移轉叢集的次要節點上的 SSISDB。 因為 Scale Out Master 服務和 SSISDB 可以個別容錯移轉，所以在容錯移轉之後可以不在相同的節點上。

![HA 伺服器設定](media/ha-server-config.PNG)

### <a name="22-include-the-dns-host-name-for-the-scale-out-master-service-in-the-cns-of-the-scale-out-master-certificate"></a>2.2 在 Scale Out Master 憑證的 CN 中包含 Scale Out Master 服務的 DNS 主機名稱

此主機名稱用於 Scale Out Master 端點中。 

![HA 主要設定](media/ha-master-config.PNG)

## <a name="3-install-scale-out-master-on-the-secondary-node"></a>3.在次要節點上安裝 Scale Out Master
在 Scale Out Master 的次要節點上，安裝 SQL Server Database Engine Services、Integration Services 和 Scale Out Master。 

使用與主要節點上所使用的相同 Scale Out Master 憑證。 使用私密金鑰來匯出主要節點上的 Scale Out Master SSL 憑證，並將它安裝至次要節點上本機電腦的根憑證存放區。 在次要節點上安裝 Scale Out Master 時選取此憑證。

![HA 主要設定 2](media/ha-master-config2.PNG)

> [!NOTE]
> 您可以對其他次要節點上的 Scale Out Master 重複這些作業，來設定多個備份 Scale Out Master。

## <a name="4-set-up-ssisdb-always-on"></a>4.設定 SSISDB AlwaysOn

遵循 [AlwaysOn for SSIS 目錄 (SSISDB)](../catalog/ssis-catalog.md#always-on-for-ssis-catalog-ssisdb) 中設定 AlwaysOn for SSISDB 的指示。

此外，您還需要建立在其中新增 SSISDB 之可用性群組的可用性群組接聽程式。 請參閱[建立或設定可用性群組接聽程式](../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)。

## <a name="5-update-the-scale-out-master-service-configuration-file"></a>5.更新 Scale Out Master 服務設定檔
更新主要和次要節點上的 Scale Out Master 服務設定檔 `\<drive\>:\Program Files\Microsoft SQL Server\140\DTS\Binn\MasterSettings.config`。 將 **SqlServerName** 更新為 [可用性群組接聽程式 DNS 名稱],[連接埠]。

## <a name="6-enable-package-execution-logging"></a>6.啟用套件執行記錄

SSISDB 中的記錄是透過自動產生其密碼來登入 **##MS_SSISLogDBWorkerAgentLogin##** 所完成。 若要讓記錄適用於所有 SSISDB 複本，請執行下列動作

### <a name="61-change-the-password-of-msssislogdbworkeragentlogin-on-the-primary-sql-server"></a>6.1 變更主要 SQL Server 上 **##MS_SSISLogDBWorkerAgentLogin##** 的密碼

### <a name="62-add-the-login-to-the-secondary-sql-server"></a>6.2 新增次要 SQL Server 的登入

### <a name="63-update-the-connection-string-used-for-logging"></a>6.3 更新用於記錄的連接字串。
呼叫含下列參數值的預存程序 `[catalog].[update_logdb_info]`：

-   `@server_name = '[Availability Group Listener DNS name],[Port]' `

-   `@connection_string = 'Data Source=[Availability Group Listener DNS name],[Port];Initial Catalog=SSISDB;User Id=##MS_SSISLogDBWorkerAgentLogin##;Password=[Password]];'`

## <a name="7-configure-the-scale-out-master-service-role-of-the-windows-failover-cluster"></a>7.設定 Windows 容錯移轉叢集的 Scale Out Master 服務角色

1.  在容錯移轉叢集管理員中，連線至 Scale Out 的叢集。選取叢集。 選取功能表中的 [動作]，然後選取 [設定角色]。

2.  在 [高可用性精靈] 對話方塊中，選取 [選取角色] 頁面上的 [泛型服務]。 在 [選取服務] 頁面上，選取 [SQL Server Integration Services Scale Out Master 14.0]。

3.  在 [用戶端存取點] 頁面上，輸入 Scale Out Master 服務的 DNS 主機名稱。

    ![HA 精靈 1](media/ha-wizard1.PNG)

4.  完成精靈。

## <a name="8-update-the-scale-out-master-address-in-ssisdb"></a>8.更新 SSISDB 中的 Scale Out Master 位址

在主要 SQL Server 上，搭配執行預存程序 `[catalog].[update_master_address]` 與參數值 `@MasterAddress = N'https://[Scale Out Master service DNS host name]:[Master Port]'`。 

## <a name="9-add-the-scale-out-workers"></a>9.新增 Scale Out Worker

現在，您可以透過 [Integration Services Scale Out Manager](integration-services-ssis-scale-out-manager.md) 的協助來新增 Scale Out Worker。 在連線頁面上輸入 `[SQL Server Availability Group Listener DNS name],[Port]`。

## <a name="next-steps"></a>後續步驟
如需詳細資訊，請參閱下列文章：
-   [Integration Services (SSIS) Scale Out Master](integration-services-ssis-scale-out-master.md)
-   [Integration Services (SSIS) Scale Out Worker](integration-services-ssis-scale-out-worker.md)