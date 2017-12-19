---
title: "SQL Server Integration Services (SSIS) Scale Out 高可用性支援 | Microsoft Docs"
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: scale-out
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: "1"
author: haoqian
ms.author: haoqian
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2202b61a9efce26edb0edcef53204351338ecee6
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="scale-out-support-for-high-availability"></a>高可用性的 Scale Out 支援

在 SSIS Scale Out 中，背景工作端高可用性的提供是透過執行含多個 Scale Out Worker 的套件。
使用 [SSIS 目錄一律開啟](../service/ssis-catalog.md#always-on-for-ssis-catalog-ssisdb)和 Windows 容錯移轉叢集可以達成主要端高可用性。 多個 Scale Out Master 執行個體裝載於 Windows 容錯移轉叢集中。 關閉主要節點上的 Scale Out Master 服務或 SSISDB 時，次要節點上的服務或 SSISDB 將繼續接受使用者要求，並與 Scale Out Worker 通訊。 

若要設定主要端高可用性，請遵循下列步驟。

## <a name="1-prerequisites"></a>1.必要條件
設定 Windows 容錯移轉叢集。 如需相關指示，請參閱 [安裝適用於 Windows Server 2012 的容錯移轉叢集功能和工具](http://blogs.msdn.com/b/clustering/archive/2012/04/06/10291601.aspx) 部落格文章。 您應該在所有叢集節點上安裝此功能和工具。

## <a name="2-install-scale-out-master-on-primary-node"></a>2.在主要節點上安裝 Scale Out Master
在 Scale Out Master 的主要節點上，安裝 Database Engine Services、Integration Services 和 Scale Out Master。 

在安裝期間，您應該 
### <a name="21-set-the-account-running-scale-out-master-service-to-a-domain-account"></a>2.1 將執行 Scale Out Master 服務的帳戶設定為網域帳戶。
此帳戶未來應該可以存取 Windows 容錯移轉叢集的次要節點上的 SSISDB。 因為 Scale Out Master 服務和 SSISDB 可以個別容錯移轉，所以可以不在相同的節點上。

![HA 伺服器設定](media/ha-server-config.PNG)

### <a name="22-include-scale-out-master-service-dns-host-name-in-the-cns-of-scale-out-master-certificate"></a>2.2 在 Scale Out Master 憑證的 CN 中包含 Scale Out Master 服務 DNS 主機名稱。

此主機名稱將用於 Scale Out Master 端點。 

![HA 主要設定](media/ha-master-config.PNG)

## <a name="3-install-scale-out-master-on-secondary-node"></a>3.在次要節點上安裝 Scale Out Master
在 Scale Out Master 的次要節點上，安裝 Database Engine Services、Integration Services 和 Scale Out Master。 

您應該使用與主要節點相同的 Scale Out Master 憑證。 使用私密金鑰來匯出主要節點上的 Scale Out Master SSL 憑證，並將它安裝至次要節點上本機機器的根憑證存放區。 安裝 Scale Out Master 時選取此憑證。

![HA 主要設定 2](media/ha-master-config2.PNG)

> [!Note]
> 您可以重複次要 Scale Out Master 的作業，來設定多個備份 Scale Out Master。

## <a name="4-set-up-ssisdb-always-on"></a>4.設定一律開啟 SSISDB

在 [SSIS 目錄一律開啟 (SSISDB)](../service/ssis-catalog.md#always-on-for-ssis-catalog-ssisdb) 中，可以看到設定 SSISDB 一律開啟的指示。

此外，您還需要建立已新增 SSISDB 之可用性群組的可用性群組接聽程式。 請參閱[建立或設定可用性群組接聽程式](../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)。

## <a name="5-update-scale-out-master-service-configuration-file"></a>5.更新相應放大主機服務設定檔
更新主要和次要節點上的相應放大主機服務設定檔：\<磁碟機\>:\Program Files\Microsoft SQL Server\140\DTS\Binn\MasterSettings.config。 將 **SqlServerName** 更新為 *[可用性群組接聽程式 DNS 名稱],[連接埠]*。

## <a name="6-enable-package-execution-logging"></a>6.啟用套件執行記錄

SSISDB 中的記錄是透過自動產生其密碼的登入 **##MS_SSISLogDBWorkerAgentLogin##** 所完成。 若要讓記錄適用於所有 SSISDB 複本，請執行下列動作。

### <a name="61-change-the-password-of-msssislogdbworkeragentlogin-on-primary-sql-server"></a>6.1 變更主要 SQL Server 上 **##MS_SSISLogDBWorkerAgentLogin##** 的密碼。
### <a name="62-add-the-login-to-secondary-sql-server"></a>6.2 新增次要 SQL Server 的登入。
### <a name="63-update-connection-string-of-logging"></a>6.3 更新記錄的連接字串。
呼叫預存程序 [catalog].[update_logdb_info]，方法是使用 

@server_name = '*[可用性群組接聽程式 DNS 名稱],[連接埠]*' 

和 @connection_string = 'Data Source=*[可用性群組接聽程式 DNS 名稱]*,*[連接埠]*;Initial Catalog=SSISDB;User Id=##MS_SSISLogDBWorkerAgentLogin##;Password=*[密碼]*];'.

## <a name="7-congifure-scale-out-master-service-role-of-windows-failover-cluster"></a>7.設定 Windows 容錯移轉叢集的 Scale Out Master 服務角色

在容錯移轉叢集管理員中，連線至相應放大的叢集。選取叢集，並按一下功能表中的 [動作]，然後按一下 [設定角色]。

在快顯的 [高可用性精靈] 中，選取 [選取角色] 頁面中的 [泛型服務]，然後在 [選取服務] 頁面中選擇 SQL Server Integration Services Scale Out Master 14.0。

在 [用戶端存取點] 頁面中，輸入 Scale Out Master 服務 DNS 主機名稱。

![HA 精靈 1](media/ha-wizard1.PNG)

完成精靈。

## <a name="8-update-master-address-in-ssisdb"></a>8.更新 SSISDB 中的主要位址

在主要 SQL Server 上，執行預存程序 [SSIS].[catalog].[update_master_address] 與參數 @MasterAddress = N'https://[Scale Out Master 服務 DNS 主機名稱]:[Master 連接埠]'。 

## <a name="9-add-scale-out-worker"></a>9.新增 Scale Out Worker

現在，您可以透過 [Scale Out Manager](integration-services-ssis-scale-out-manager.md) 的協助來新增 Scale Out Worker。 在連線頁面中，輸入 [SQL Server 可用性群組接聽程式 DNS 名稱],[連接埠*]*。




