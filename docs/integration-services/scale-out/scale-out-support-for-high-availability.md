---
title: "SQL Server Integration Services (SSIS) 向外延展的高可用性支援 |Microsoft 文件"
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: 1
author: haoqian
ms.author: haoqian
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 2405235bcfa09d2cc49e007f4eae6975d9ebf7a5
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="scale-out-support-for-high-availability"></a>向外高可用性支援

在 SSIS 向外工作者端提供高可用性是透過執行多個標尺出工作者的封裝。
主機端的高可用性達成與[Alwayson 的 SSIS 目錄](../service/ssis-catalog.md#always-on-for-ssis-catalog-ssisdb)和 Windows 容錯移轉叢集。 Windows 容錯移轉叢集中裝載多個標尺出主要執行個體。 當標尺出主要服務或 SSISDB 主要節點上已關閉時，服務或在次要節點上的 SSISDB 會繼續接受使用者要求，並與標尺出工作者通訊。 

若要設定主要端的高可用性，請遵循下列步驟。

## <a name="1-prerequisites"></a>1.필수 구성 요소
設定 Windows 容錯移轉叢集。 如需相關指示，請參閱 [安裝適用於 Windows Server 2012 的容錯移轉叢集功能和工具](http://blogs.msdn.com/b/clustering/archive/2012/04/06/10291601.aspx) 部落格文章。 您應該在所有叢集節點上安裝此功能和工具。

## <a name="2-install-scale-out-master-on-primary-node"></a>2.在主要節點上安裝出主要刻度
主要節點上安裝 Database Engine Services、 Integration Services 和標尺出 Master 出主要刻度。 

在安裝期間，您應該 
### <a name="21-set-the-account-running-scale-out-master-service-to-a-domain-account"></a>2.1 設定為網域帳戶執行標尺出主機服務的帳戶。
此帳戶應該能夠在未來存取 Windows 容錯移轉叢集中的第二個節點上的 SSISDB。 標尺出主要服務和 SSISDB 可以容錯移轉的同時，因為它們可能不是相同的節點上。

![HA 伺服器組態](media/ha-server-config.PNG)

### <a name="22-include-scale-out-master-service-dns-host-name-in-the-cns-of-scale-out-master-certificate"></a>2.2 出主要包含小數位數服務 DNS 主機名稱中的 Cn 的標尺出主要憑證。

這個主機名稱將用於標尺出主要端點。 

![HA 主要設定](media/ha-master-config.PNG)

## <a name="3-install-scale-out-master-on-secondary-node"></a>3.在次要節點上安裝出主要刻度
第二個節點上安裝 Database Engine Services、 Integration Services 和標尺出 Master 出主要刻度。 

您應該使用相同的標尺出主要憑證與主要節點。 匯出私密金鑰主要節點上的標尺出主要 SSL 憑證，並將它安裝到 loacl 機器次要節點上的根憑證存放區。 安裝小數位數出 Master 時，請選取此憑證。

![HA 主要設定 2](media/ha-master-config2.PNG)

> [!Note]
> 您可以設定備份多個標尺出母片重複第二個標尺出主要的作業。

## <a name="4-set-up-ssisdb-always-on"></a>4.SSISDB 一律上設定

設定指示一律上的 SSISDB 可以看到在[Alwayson 的 SSIS 目錄 (SSISDB)](../service/ssis-catalog.md#always-on-for-ssis-catalog-ssisdb)。

此外，您要建立可用性 gourp SSISDB 加入至可用性群組接聽程式。 請參閱[建立或設定可用性群組接聽程式](../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)。

## <a name="5-update-scale-out-master-service-configuration-file"></a>5.更新標尺出主要服務組態檔
更新的標尺出主要服務組態檔，\<驅動程式\>: \Program Files\Microsoft SQL Server\140\DTS\Binn\MasterSettings.config 主要和次要節點上的。 更新**SqlServerName**至*[可用性群組接聽程式 DNS 名稱]，[連接埠]*。

## <a name="6-enable-package-execution-logging"></a>6.啟用封裝執行記錄

在 SSISDB 中記錄由登入**# # MS_SSISLogDBWorkerAgentLogin # #**，密碼是自動產生。 若要讓記錄適用於 SSISDB 的所有複本，執行下列動作。

### <a name="61-change-the-password-of-msssislogdbworkeragentlogin-on-primary-sql-server"></a>6.1 變更的密碼**# # MS_SSISLogDBWorkerAgentLogin # #**主要 Sql 伺服器上。
### <a name="62-add-the-login-to-secondary-sql-server"></a>6.2 加入次要 Sql Server 的登入。
### <a name="63-update-connection-string-of-logging"></a>6.3 更新連接字串的記錄。
呼叫預存程序 [catalog]。[update_logdb_info] 與 

@server_name= '*[可用性群組接聽程式 DNS 名稱]，[連接埠]*' 

和@connection_string= ' 資料來源 =*[可用性群組接聽程式 DNS 名稱]*，*[Port]*; Initial Catalog = SSISDB;使用者 Id = # # MS_SSISLogDBWorkerAgentLogin # #。密碼 =*[Password]*];'。

## <a name="7-congifure-scale-out-master-service-role-of-windows-failover-cluster"></a>7.Windows 容錯移轉叢集的 Congifure 標尺出主要服務角色

在容錯移轉叢集管理員，連線到叢集的延展輸出。 選取叢集，然後按一下**動作**功能表中，然後**設定角色...**.

在推出向上**高可用性精靈**，選取**泛型服務**中**選取角色**頁面上，然後選擇 SQL Server Integration Services 標尺出主要 14.0 中**選取服務**頁面。

在**用戶端存取點**頁面上，輸入小數位數出主要服務的 DNS 主機名稱。

![高可用性精靈 1](media/ha-wizard1.PNG)

完成精靈作業。

## <a name="8-update-master-address-in-ssisdb"></a>8.更新主要在 SSISDB 中的位址

在主要 SQL 伺服器上，執行預存程序 [SSIS]。[目錄]。[update_master_address] 參數@MasterAddress= N'https: / / [標尺出主要服務 DNS 主機名稱]: [主要連接埠]'。 

## <a name="9-add-scale-out-worker"></a>9.加入向外延展背景工作

現在，您可以加入標尺出工作者的協助[標尺出管理員](integration-services-ssis-scale-out-manager.md)。 輸入*[SQL Server 可用性群組接聽程式 DNS 名稱]*，*[Port]*連接頁面中。





