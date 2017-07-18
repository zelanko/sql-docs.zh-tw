---
title: "PolyBase 安裝 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 08/31/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-polybase
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- PolyBase, installation
ms.assetid: 3a1e64be-9bfc-4408-accd-35990e1a6b52
caps.latest.revision: 25
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: dd279b20fdf0f42d4b44843244aeaf6f19f04718
ms.openlocfilehash: 0c39bbf997fb5041a1fc4ea55699fbb3a40e3d75
ms.contentlocale: zh-tw
ms.lasthandoff: 07/14/2017

---
# <a name="polybase-installation"></a>安裝 PolyBase
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  若要安裝 SQL Server 試用版，請移至 [SQL Server 評估版](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016)。 
  
## <a name="prerequisites"></a>必要條件  
  
-   64 位元 SQL Server 評估版  
  
-   Microsoft .NET Framework 4.5。  
  
-   Oracle Java SE RunTime Environment (JRE) 7.51 版或更新版本 (64 位元) ( [JRE](http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html) 或 [Server JRE](http://www.oracle.com/technetwork/java/javase/downloads/server-jre8-downloads-2133154.html) 皆適用)。 前往 [Java SE Downloads](http://www.oracle.com/technetwork/java/javase/downloads/index.html)(Java SE 下載)。 如果 JRE 不存在，安裝程式將會失敗。  
  
-   最小記憶體︰4 GB  
  
-   最小硬碟空間︰2 GB  
  
-   必須啟用 TCP/IP 連線。 (請參閱 [啟用或停用伺服器網路通訊協定](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)。)SQL Server Developer 和 Express 版預設會停用 TCP/IP 連線能力。 必須手動啟用此功能，PolyBase 才能正常運作。
  
 **注意**  
  
 每部電腦只能在一個 SQL Server 執行個體上安裝 PolyBase。  
  
## <a name="single-node-or-polybase-scaleout-group"></a>單一節點或 PolyBase 向外延展群組
在 SQL Server 執行個體上開始安裝 PolyBase 時，最好規劃是要單一節點安裝還是 PolyBase 向外延展群組安裝。 針對 PolyBase 向外延展群組，您需要確定： 
- 相同網域上的所有電腦。
- 您可以在安裝期間使用相同的服務帳戶和密碼。
- 而 SQL Server 執行個體可以透過網路彼此通訊。

PolyBase 一旦安裝為獨立項目或安裝於向外延展群組中，就無法再進行變更。 您必須將功能解除安裝之後再重新安裝，才能變更此設定。

## <a name="install-using-the-installation-wizard"></a>使用安裝精靈安裝  
  
1.  執行 [SQL Server 安裝中心]。 插入 SQL Server 安裝媒體，然後按兩下 [Setup.exe]。  
  
2.  按一下 [安裝] ，然後按一下 [新的獨立 SQL Server 安裝或加入功能] 。  
  
3.  在 [特徵選取] 頁面上，選取 [外部資料的 PolyBase 查詢服務] 。  
  
4.  在 [伺服器組態] 頁面上，將 **SQL Server PolyBase 引擎服務** 和 SQL Server PolyBase 資料移動服務設定為在同一個帳戶下執行。  
  
    > **重要！** 在 PolyBase 向外延展群組中，所有節點上的 PolyBase 引擎和 PolyBase 資料移動服務必須在同一個網域帳戶執行。  
    > 請參閱＜向外擴充 PolyBase＞。  
  
5.  在 [PolyBase 組態頁面] 上，選取兩個選項的其中一個。 如需詳細資訊，請參閱 [PolyBase 向外延展群組](../../relational-databases/polybase/polybase-scale-out-groups.md)。  
  
    -   使用 SQL Server 執行個體作為已啟用 PolyBase 的獨立執行個體。  
  
         選擇此選項，將 SQL Server 執行個體當作獨立的前端節點使用。  
  
    -   使用 SQL Server 執行個體做為 PolyBase 向外延展群組的一部分。  選取此選項會開啟防火牆，以允許連至 SQL Server Database Engine、SQL Server PolyBase Engine、SQL Server PolyBase Data Movement Service 及 SQL Browser 的連入連線。 開啟防火牆會允許從 PolyBase 向外延展群組中其他節點連入的連線。  
  
         選取此選項也會啟用 Microsoft Distributed Transaction Coordinator (MSDTC) 防火牆連線，並修改 MSDTC 登錄設定。  
  
6.  在 [PolyBase 組態] 頁面上，指定含至少六個連接埠的連接埠範圍。 SQL Server 安裝程式將配置該範圍內前六個可用的連接埠。  
  
##  <a name="installing"></a> 使用命令提示字元安裝  
 使用此資料表中的值來建立安裝指令碼。 **SQL Server PolyBase 引擎** 和 **SQL Server PolyBase 資料移動服務** 這兩項服務必須在同一個帳戶下執行。 在 PolyBase 向外延展群組中，所有節點上的 PolyBase 服務必須在同一個網域帳戶下執行。  
  
|SQL Server 元件|參數和值|描述|  
|--------------------------|--------------------------|-----------------|  
|SQL Server 安裝程式控制|**必要項**<br /><br /> /FEATURES=PolyBase|選取 PolyBase 功能。|  
|SQL Server PolyBase 引擎|**選擇性**<br /><br /> /PBENGSVCACCOUNT|指定引擎服務的帳戶。 預設值是 **NT Authority\NETWORK SERVICE**。|  
|SQL Server PolyBase 引擎|**選擇性**<br /><br /> /PBENGSVCPASSWORD|指定引擎服務帳戶的密碼。|  
|SQL Server PolyBase 引擎|**選擇性**<br /><br /> /PBENGSVCSTARTUPTYPE|指定 PolyBase 引擎服務的啟動模式︰Automatic (自動，預設值)、Disabled (停用) 以及 Manual (手動)。|  
|SQL Server PolyBase 資料移動服務|**選擇性**<br /><br /> /PBDMSSVCACCOUNT|指定資料移動服務的帳戶。 預設值是 **NT Authority\NETWORK SERVICE**。|  
|SQL Server PolyBase 資料移動服務|**選擇性**<br /><br /> /PBDMSSVCPASSWORD|指定資料移動帳戶的密碼。|  
|SQL Server PolyBase 資料移動服務|**選擇性**<br /><br /> /PBDMSSVCSTARTUPTYPE|指定資料移動服務的啟動模式︰Automatic (自動，預設值)、Disabled (停用) 以及 Manual (手動)。|  
|PolyBase|**選擇性**<br /><br /> /PBSCALEOUT|指定 SQL Server 執行個體是否會用作 PolyBase 向外延展計算群組的一部分。 <br />支援的值： **True**、 **False**|  
|PolyBase|**選擇性**<br /><br /> /PBPORTRANGE|為 PolyBase 服務指定含至少 6 個連接埠的連接埠範圍。 範例：<br /><br /> `/PBPORTRANGE=16450-16460`|  
  
 **範例**  
  
 以下顯示的是安裝指令碼範例。  
  
```  
  
Setup.exe /Q /ACTION=INSTALL /IACCEPTSQLSERVERLICENSETERMS /FEATURES=SQLEngine,Polybase   
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="\<fabric-domain>\Administrator"   
/INSTANCEDIR="C:\Program Files\Microsoft SQL Server" /PBSCALEOUT=TRUE   
/PBPORTRANGE=16450-16460 /SECURITYMODE=SQL /SAPWD="<StrongPassword>"   
/PBENGSVCACCOUNT="<DomainName>\<UserName>" /PBENGSVCPASSWORD="<StrongPassword>"   
/PBDMSSVCACCOUNT="<DomainName>\<UserName>" /PBDMSSVCPASSWORD="<StrongPassword>"  
  
```  
  
## <a name="post-installation-notes"></a>安裝後注意事項  
 PolyBase 會安裝三個使用者資料庫：DWConfiguration、DWDiagnostics 和 DWQueue。   這些資料庫會用於 PolyBase，不應該予以改變或刪除。  
  
### <a name="how-to-confirm-installation"></a>如何確認安裝  
 執行下列命令。 如果已安裝 PolyBase 會傳回 1，否則會傳回 0。  
  
```tsql  
SELECT SERVERPROPERTY ('IsPolybaseInstalled') AS IsPolybaseInstalled;  
```  
  
### <a name="firewall-rules"></a>防火牆規則  
 SQL Server PolyBase 安裝程式會在電腦上建立下列防火牆規則。  
  
-   SQL Server PolyBase – Database Engine - \<SQLServerInstanceName> (TCP-In)  
  
-   SQL Server PolyBase – PolyBase 服務 - \<SQLServerInstanceName> (TCP-In)  
  
-   SQL Server PolyBase - SQL Browser - (UDP-In)  
  
 進行安裝時，如果您選擇使用 SQL Server 執行個體做為 PolyBase 向外擴充群組的一部分，則這些規則會啟用並開啟防火牆以允許連入 SQL Server Database Engine、SQL Server PolyBase Engine、SQL Server PolyBase Data Movement Service 和 SQL Browser 的連線。 不過，如果安裝期間防火牆服務未在電腦上執行，SQL Server 安裝程式會無法啟用這些規則。 在這樣的情況下，安裝之後您必須啟動電腦上的防火牆服務並啟用這些規則。  
  
#### <a name="to-enable-the-firewall-rules"></a>啟用防火牆規則  
  
-   開啟 [控制台] 。  
  
-   按一下 [系統及安全性] ，然後按一下 [Windows 防火牆] 。  
  
-   按一下 [進階設定] ，然後按一下 [輸入規則] 。  
  
-   以滑鼠右鍵按一下已停用的規則，然後按一下 [啟用規則]。  
  
### <a name="polybase-service-accounts"></a>PolyBase 服務帳戶
若要變更 PolyBase 引擎和 PolyBase 資料移動服務的服務帳戶，請解除安裝並重新安裝 PolyBase 功能。
   
## <a name="next-steps"></a>後續的步驟  
 請參閱 [PolyBase configuration](../../relational-databases/polybase/polybase-configuration.md)。  
  
  

