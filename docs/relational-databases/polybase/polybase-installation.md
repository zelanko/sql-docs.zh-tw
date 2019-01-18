---
title: 在 Windows 上安裝 PolyBase | Microsoft Docs
ms.custom: ''
ms.date: 09/24/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: polybase
ms.topic: conceptual
helpviewer_keywords:
- PolyBase, installation
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 3c08f8cb48e22ba5ca1546f9fcca63f77868b356
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/11/2018
ms.locfileid: "53208796"
---
# <a name="install-polybase-on-windows"></a>在 Windows 上安裝 PolyBase

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

若要安裝 SQL Server 試用版，請移至 [SQL Server 評估版](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016)。 
   
## <a name="prerequisites"></a>Prerequisites  
   
- 64 位元 SQL Server Evaluation 版。  
   
- Microsoft .NET Framework 4.5。  

- Oracle Java SE Runtime Environment (JRE)。 支援版本 7 (從 7.51 開始) 和 8。 [JRE](https://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html) 和 [Server JRE](https://www.oracle.com/technetwork/java/javase/downloads/server-jre8-downloads-2133154.html) 都可。 前往 [Java SE Downloads](https://www.oracle.com/technetwork/java/javase/downloads/index.html)(Java SE 下載)。 如果 JRE 不存在，安裝程式會失敗。 不支援 JRE9 和 JRE10。

- 最小記憶體：4 GB。 
   
- 最小硬碟空間：2 GB。
  
- 建議事項：至少 16 GB RAM。
   
- 必須啟用 TCP/IP，PolyBase 才能正常運作。 預設會在 SQL Server Developer 和 Express 版本以外的所有 SQL Server 版本上啟用 TCP/IP。 若要讓 PolyBase 在 Developer 和 Express 版本上正常運作，您必須啟用 TCP/IP 連線。 請參閱[啟用或停用伺服器網路通訊協定](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)。

- MSVC++ 2012。 

> [!NOTE]
> 
> 每部電腦只能在一個 SQL Server 執行個體上安裝 PolyBase。
> 
> [!IMPORTANT]
> 
> 若要針對 Hadoop 使用計算下推功能，目標 Hadoop 叢集必須具有 HDFS、YARN 和 MapReduce 的核心元件，並已啟用作業記錄伺服器。 PolyBase 透過 MapReduce 來提交下推查詢，並從作業記錄伺服器提取狀態。 如果沒有其中一個元件，則查詢會失敗。
  
## <a name="single-node-or-polybase-scale-out-group"></a>單一節點或 PolyBase 向外延展群組

在 SQL Server 執行個體上安裝 PolyBase 之前，請決定您想要單一節點安裝還是 [PolyBase 向外延展群組](../../relational-databases/polybase/polybase-scale-out-groups.md)。

若是 PolyBase 向外延展群組，請確定：

- 相同網域上的所有電腦。
- 您在進行 PolyBase 安裝期間使用相同的服務帳戶和密碼。
- 您的 SQL Server 執行個體可透過網路彼此通訊。
- SQL Server 執行個體皆為同一個 SQL Server 版本。

將 PolyBase 安裝為獨立項目或安裝於向外延展群組之後，就無法再進行變更。 若要變更此設定，您必須將功能解除安裝之後再重新安裝。

## <a name="use-the-installation-wizard"></a>使用安裝精靈
   
1. 執行 SQL Server setup.exe。   
   
2. 選取 [安裝]，然後選取 [新的獨立 SQL Server 安裝或新增功能]。  
   
3. 在 [功能選取] 頁面上，選取 [適用於外部資料的 PolyBase 查詢服務]。  

   ![PolyBase 服務](../../relational-databases/polybase/media/install-wizard.png "PolyBase 服務")  
   
4. 在 [伺服器設定] 頁面上，將 [SQL Server PolyBase 引擎服務] 和 [SQL Server PolyBase 資料移動服務] 設定為在同一個網域帳戶下執行。  
   
   > [!IMPORTANT] 
   >
   >在 PolyBase 向外延展群組中，所有節點上的 PolyBase 引擎和 PolyBase 資料移動服務必須在同一個網域帳戶執行。 請參閱 [PolyBase 向外延展群組](#Enable)。
   
5. 在 [PolyBase 設定] 頁面上，選取兩個選項的其中一個。 如需詳細資訊，請參閱 [PolyBase 向外延展群組](../../relational-databases/polybase/polybase-scale-out-groups.md)。  
   
   - 使用 SQL Server 執行個體作為已啟用 PolyBase 的獨立執行個體。  
   
     選擇此選項以使用 SQL Server 執行個體作為獨立前端節點。  
   
   - 使用 SQL Server 執行個體做為 PolyBase 向外延展群組的一部分。 此選項會開啟防火牆，以允許連入連線。 允許連至 SQL Server 資料庫引擎、SQL Server PolyBase 引擎、SQL Server PolyBase 資料移動服務及 SQL Browser 的連線。 防火牆也會允許從 PolyBase 向外延展群組中其他節點連入的連線。  
   
     此選項也會啟用 Microsoft Distributed Transaction Coordinator (MSDTC) 防火牆連線，並修改 MSDTC 登錄設定。  
   
6. 在 [PolyBase 設定] 頁面上，指定至少具有六個連接埠的連接埠範圍。 SQL Server 安裝程式會配置該範圍內前六個可用的連接埠。  

   > [!IMPORTANT]
   >
   > 安裝完成後，您必須[啟用 PolyBase 功能](#enable)。


##  <a name="installing"></a> 使用命令提示字元

使用此資料表中的值來建立安裝指令碼。 SQL Server PolyBase 引擎和 SQL Server PolyBase 資料移動服務必須在同一個帳戶下執行。 在 PolyBase 向外延展群組中，所有節點上的 PolyBase 服務必須在同一個網域帳戶下執行。  
   
<!--SQL Server 2016/2017-->
::: moniker range="= sql-server-2016 || = sql-server-2017"

|SQL Server 元件|參數和值|Description|  
|--------------------------|--------------------------|-----------------|  
|SQL Server 安裝程式控制|**必要項**<br /><br /> /FEATURES=PolyBase|選取 PolyBase 功能。|  
|SQL Server PolyBase 引擎|**選擇性**<br /><br /> /PBENGSVCACCOUNT|指定引擎服務的帳戶。 預設值是 **NT Authority\NETWORK SERVICE**。|  
|SQL Server PolyBase Engine|**選擇性**<br /><br /> /PBENGSVCPASSWORD|指定引擎服務帳戶的密碼。|  
|SQL Server PolyBase Engine|**選擇性**<br /><br /> /PBENGSVCSTARTUPTYPE|指定 PolyBase 引擎的啟動模式：Automatic (自動，預設)、Disabled (停用) 以及 Manual (手動)。|  
|SQL Server PolyBase 資料移動 |**選擇性**<br /><br /> /PBDMSSVCACCOUNT|指定資料移動服務的帳戶。 預設是 **NT Authority\NETWORK SERVICE**。|  
|SQL Server PolyBase 資料移動 |**選擇性**<br /><br /> /PBDMSSVCPASSWORD|指定資料移動帳戶的密碼。|  
|SQL Server PolyBase 資料移動 |**選擇性**<br /><br /> /PBDMSSVCSTARTUPTYPE|指定資料移動服務的啟動模式：Automatic (自動，預設)、Disabled (停用) 以及 Manual (手動)。|  
|PolyBase|**選擇性**<br /><br /> /PBSCALEOUT|指定 SQL Server 執行個體是否會用作 PolyBase 向外延展計算群組的一部分。 <br />支援的值：True、False。|  
|PolyBase|**選擇性**<br /><br /> /PBPORTRANGE|為 PolyBase 服務指定至少具有六個連接埠的連接埠範圍。 範例<br /><br /> `/PBPORTRANGE=16450-16460`|  

::: moniker-end
<!--SQL Server 2019-->
::: moniker range=">= sql-server-ver15 || =sqlallproducts-allversions"

|SQL Server 元件|參數和值|Description|  
|--------------------------|--------------------------|-----------------|  
|SQL Server 安裝程式控制|**必要**<br /><br /> /FEATURES=PolyBaseCore, PolyBaseJava, PolyBase | PolyBaseCore 會安裝所有 PolyBase 功能的支援，除了 Hadoop 連線能力以外。 PolyBaseJava 可啟用 Hadoop 連線能力。 PolyBase 兩種都會安裝。 |  
|SQL Server PolyBase Engine|**選擇性**<br /><br /> /PBENGSVCACCOUNT|指定引擎服務的帳戶。 預設值是 **NT Authority\NETWORK SERVICE**。|  
|SQL Server PolyBase Engine|**選擇性**<br /><br /> /PBENGSVCPASSWORD|指定引擎服務帳戶的密碼。|  
|SQL Server PolyBase Engine|**選擇性**<br /><br /> /PBENGSVCSTARTUPTYPE|指定 PolyBase 引擎的啟動模式：Automatic (自動，預設)、Disabled (停用) 以及 Manual (手動)。|  
|SQL Server PolyBase 資料移動 |**選擇性**<br /><br /> /PBDMSSVCACCOUNT|指定資料移動服務的帳戶。 預設是 **NT Authority\NETWORK SERVICE**。|  
|SQL Server PolyBase 資料移動 |**選擇性**<br /><br /> /PBDMSSVCPASSWORD|指定資料移動帳戶的密碼。|  
|SQL Server PolyBase 資料移動 |**選擇性**<br /><br /> /PBDMSSVCSTARTUPTYPE|指定資料移動服務的啟動模式：Automatic (自動，預設)、Disabled (停用) 以及 Manual (手動)。|  
|PolyBase|**選擇性**<br /><br /> /PBSCALEOUT|指定 SQL Server 執行個體是否會用作 PolyBase 向外延展計算群組的一部分。 <br />支援的值：True、False。|  
|PolyBase|**選擇性**<br /><br /> /PBPORTRANGE|為 PolyBase 服務指定至少具有六個連接埠的連接埠範圍。 範例<br /><br /> `/PBPORTRANGE=16450-16460`|  

::: moniker-end

安裝完成後，您必須[啟用 PolyBase 功能](#enable)。



**範例**

此範例顯示範例安裝指令碼。  

```cmd
   
Setup.exe /Q /ACTION=INSTALL /IACCEPTSQLSERVERLICENSETERMS /FEATURES=SQLEngine,PolyBase   
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="\<fabric-domain>\Administrator"   
/INSTANCEDIR="C:\Program Files\Microsoft SQL Server" /PBSCALEOUT=TRUE   
/PBPORTRANGE=16450-16460 /SECURITYMODE=SQL /SAPWD="<StrongPassword>"   
/PBENGSVCACCOUNT="<DomainName>\<UserName>" /PBENGSVCPASSWORD="<StrongPassword>"   
/PBDMSSVCACCOUNT="<DomainName>\<UserName>" /PBDMSSVCPASSWORD="<StrongPassword>"  
   
```  

## <a id="enable"></a> 啟用 PolyBase

安裝之後，您必須啟用 PolyBase 來存取其功能。 若要連線到 SQL Server 2019 CTP 2.0，您必須在安裝後啟用 PolyBase。 使用下列 Transact-SQL 命令。


```sql
exec sp_configure @configname = 'polybase enabled', @configvalue = 1;
RECONFIGURE [ WITH OVERRIDE ]  ;
```
接著必須重新啟動執行個體。


## <a name="post-installation-notes"></a>安裝後的注意事項  

PolyBase 會安裝三個使用者資料庫：DWConfiguration、DWDiagnostics 和 DWQueue。 這些資料庫會用於 PolyBase。 請勿予以改變或刪除。  
   
### <a id="confirminstall"></a> 如何確認安裝  

執行下列命令。 如果已安裝 PolyBase，則會傳回 1。 否則為 0。  

```sql  
SELECT SERVERPROPERTY ('IsPolyBaseInstalled') AS IsPolyBaseInstalled;  
```  

### <a name="firewall-rules"></a>防火牆規則  

SQL Server PolyBase 安裝程式會在電腦上建立下列防火牆規則：  
   
- SQL Server PolyBase - Database Engine - \<SQLServerInstanceName> (TCP-In)  
   
- SQL Server PolyBase - PolyBase 服務 - \<SQLServerInstanceName> (TCP-In)  

- SQL Server PolyBase - SQL Browser - (UDP-In)  
   
安裝時，如果使用 SQL Server 執行個體作為 PolyBase 向外延展群組的一部分，則會啟用這些規則。 防火牆會開啟，以允許連入連線。 允許連至 SQL Server 資料庫引擎、SQL Server PolyBase 引擎、SQL Server PolyBase 資料移動服務及 SQL Browser 的連線。 如果電腦上的防火牆服務在安裝期間並未執行，SQL Server 安裝程式會無法啟用這些規則。 在這樣的情況下，安裝之後請啟動電腦上的防火牆服務並啟用這些規則。  
   
#### <a name="to-enable-the-firewall-rules"></a>啟用防火牆規則  

1. 開啟 [控制台]。  

2. 選取 [系統及安全性]，然後選取 [Windows 防火牆]。  
   
3. 選取 [進階設定]，然後選取 [輸入規則]。  
   
4. 以滑鼠右鍵按一下已停用的規則，然後選取 [啟用規則]。  
   
### <a name="polybase-service-accounts"></a>PolyBase 服務帳戶

若要變更 PolyBase 引擎和 PolyBase 資料移動服務的服務帳戶，請解除安裝並重新安裝 PolyBase 功能。

## <a name="next-steps"></a>後續步驟  

請參閱 [PolyBase configuration](../../relational-databases/polybase/polybase-configuration.md)。
