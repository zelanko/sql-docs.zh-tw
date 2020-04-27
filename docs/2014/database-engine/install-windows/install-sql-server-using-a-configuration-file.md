---
title: 使用設定檔安裝 SQL Server 2014 |Microsoft Docs
ms.custom: ''
ms.date: 01/20/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: a832153a-6775-4bed-83f0-55790766d885
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 38cd8aeb157a94a28b1cfd831bcfacfb3e93ea6f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62775281"
---
# <a name="install-sql-server-2014-using-a-configuration-file"></a>使用組態檔安裝 SQL Server 2014
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式可供您根據系統預設值與執行階段輸入，產生組態檔。 您可以使用相同的設定，於整個企業中利用組態檔部署 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 您也可以透過建立啟動 Setup.exe 的批次檔，在企業中將手動安裝標準化。  
  
 安裝程式僅支援透過命令提示字元使用組態檔。 使用組態檔時，參數的處理順序如下所述：  
  
-   組態檔會覆寫封裝中的預設值  
  
-   命令列的值會覆寫組態檔中的值  
  
 組態檔可用來追蹤每個安裝的參數和值。 這點會讓組態檔適用於驗證和稽核安裝。  
  
## <a name="configuration-file-structure"></a>組態檔結構  
 ConfigurationFile.ini 檔案是包含參數 (名稱/值組) 和描述性註解的文字檔。  
  
 下面是 ConfigurationFile.ini 檔案的範例：  
  
```  
; Microsoft SQL Server Configuration file  
[OPTIONS]  
; Specifies a Setup work flow, like INSTALL, UNINSTALL, or UPGRADE.   
; This is a required parameter.   
ACTION="Install"  
; Specifies features to install, uninstall, or upgrade.   
; The list of top-level features include SQL, AS, RS, IS, and Tools.   
; The SQL feature will install the database engine, replication, and full-text.   
; The Tools feature will install Management Tools, Books online,   
; SQL Server Data Tools, and other shared components.   
FEATURES=SQL,Tools  
```  
  
#### <a name="how-to-generate-a-configuration-file"></a>如何產生組態檔  
  
1.  插入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝媒體。 在根資料夾中，按兩下 Setup.exe。 若要從網路共用進行安裝，請找出共用上的根資料夾，然後按兩下 Setup.exe。  
  
    > [!NOTE]  
    >  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express Edition 安裝程式不會自動建立設定檔。 下列命令將會啟動安裝程式並建立設定檔。  
    >   
    >  SETUP.exe /UIMODE=Normal /ACTION=INSTALL  
  
2.  遵循精靈的指示，直到 **[準備安裝]** 頁面。 組態檔的路徑已指定於 **[準備安裝]** 頁面的 [組態檔路徑] 區段中。 如需有關如何安裝[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的詳細資訊，請參閱[install SQL Server 2014 From the 安裝 Wizard &#40;安裝程式&#41;](install-sql-server-from-the-installation-wizard-setup.md)。  
  
3.  取消安裝程式而不實際完成安裝，即可產生 INI 檔案。  
  
    > [!NOTE]  
    >  安裝程式基礎結構會針對已執行的動作寫出所有適當的參數，但密碼等機密資訊除外。 /IAcceptSQLServerLicenseTerms 參數也不會寫出至組態檔，而且需要修改組態檔或在命令提示字元中提供某個值。 如需詳細資訊，請參閱[從命令提示字元安裝 SQL Server 2014](install-sql-server-from-the-command-prompt.md)。 此外，若為通常不會透過命令提示字元提供值的布林值參數，系統就會包含一個值。  
  
## <a name="using-the-configuration-file-to-install-ssnoversion"></a>使用組態檔安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 您只能針對命令列安裝使用組態檔。  
  
> [!NOTE]  
>  如果您需要對組態檔進行變更，我們建議您製作副本並使用此副本進行變更。  
  
#### <a name="how-to-use-a-configuration-file-to-install-a-stand-alone-ssnoversion-instance"></a>如何使用組態檔安裝獨立式 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。  
  
-   透過命令提示字元執行安裝，並使用*ConfigurationFile*參數提供 ConfigurationFile。  
  
#### <a name="how-to-use-a-configuration-file-to-prepare-and-complete-an-image-of-a-stand-alone-ssnoversion-instance-sysprep"></a>如何使用組態檔準備及完成獨立式 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體 (SysPrep) 的映像  
  
1.  若要在同一部電腦上準備一個或多個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體並進行設定。  
  
    -   從安裝中心的 [進階]**** 頁面執行 [準備 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 獨立執行個體的映像]****，並擷取備妥的映像組態檔。  
  
    -   使用相同的準備映像組態檔當做範本，以便準備其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。  
  
    -   從 [安裝中心] 的 [進階]**** 頁面執行 [完成備妥的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 獨立執行個體的映像]****，在電腦上設定備妥的執行個體。  
  
2.  若要使用 Windows SysPrep 工具來準備作業系統的映像，包括未設定的已備妥 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。  
  
    -   從 [安裝中心] 的 [進階] 頁面執行 [準備 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 獨立執行個體的映像]****，並擷取備妥的映像組態檔。  
  
    -   從 [安裝中心] 的 [進階]**** 頁面執行 [完成備妥的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 獨立執行個體的映像]****，但在擷取完成的組態檔之後，在 [準備開始完成]**** 頁面上取消它。  
  
    -   完成映像組態檔可以與 Windows 映像儲存在一起，以便自動化已備妥執行個體的組態設定作業。  
  
#### <a name="how-to-install-a-ssnoversion-failover-cluster-using-the-configuration-file"></a>如何使用組態檔安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 容錯移轉叢集  
  
1.  整合式安裝選項 (在節點上建立單一節點容錯移轉叢集並且在其他節點上執行 AddNode)：  
  
    -   執行「安裝容錯移轉叢集」選項並且擷取列出所有安裝設定的組態檔。  
  
    -   透過提供 *ConfigurationFile* 參數，執行命令列容錯移轉叢集安裝。  
  
    -   在要加入的其他節點上，執行 AddNode 來擷取適用於現有容錯移轉叢集的 ConfigurationFile.ini 檔案。  
  
    -   透過使用 ConfigurationFile 參數來提供相同的組態檔，在即將聯結容錯移轉叢集的所有其他節點上執行命令列 AddNode。  
  
2.  進階安裝選項 (在所有容錯移轉叢集節點上準備容錯移轉叢集。然後，準備所有節點之後，在擁有共用磁碟的節點上執行「完成」)：  
  
    -   在其中一個節點上執行 **[準備]** ，然後擷取 ConfigurationFile.ini 檔案。  
  
    -   在即將針對容錯移轉叢集準備的所有節點上，提供相同的 ConfigurationFile.ini 檔案給安裝程式。  
  
    -   備妥所有節點之後，請在擁有共用磁碟的節點上執行「完成容錯移轉叢集」作業，並且擷取 ConfigurationFile.ini 檔案。  
  
    -   然後，您就可以提供這個 ConfigurationFile.ini 檔案來完成容錯移轉叢集。  
  
#### <a name="how-to-add-or-remove-a-node-to-a-ssnoversion-failover-cluster-using-the-configuration-file"></a>如何使用組態檔為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 容錯移轉叢集加入或移除一個節點  
  
-   如果您擁有先前用來在容錯移轉叢集中加入節點或移除節點的組態檔，就可以重複使用相同的檔案來加入或移除其他節點。  
  
#### <a name="how-to-upgrade-a-ssnoversion-failover-cluster-using-the-configuration-file"></a>如何使用組態檔升級 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 容錯移轉叢集  
  
1.  在被動節點上執行「升級」，然後擷取 ConfigurationFile.ini 檔案。 您可以透過執行實際升級或在結束時退出而不進行實際升級，完成此作業。  
  
2.  在要升級的所有其他節點上，提供 ConfigurationFile.ini 檔案來完成此程序。  
  
## <a name="sample-syntax"></a>範例語法  
 下面是有關如何使用組態檔的部分範例：  
  
-   若要在命令提示字元中指定組態檔：  
  
```  
Setup.exe /ConfigurationFile=MyConfigurationFile.INI  
```  
  
-   若要在命令提示字元而非組態檔中指定密碼：  
  
```  
Setup.exe /SQLSVCPASSWORD="************" /AGTSVCPASSWORD="************" /ASSVCPASSWORD="************" /ISSVCPASSWORD="************" /RSSVCPASSWORD="************" /ConfigurationFile=MyConfigurationFile.INI  
```  
  
## <a name="see-also"></a>另請參閱  
 [從命令提示字元安裝 SQL Server 2014](install-sql-server-from-the-command-prompt.md)   
 [SQL Server 容錯移轉叢集安裝](../../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md)   
 [升級 SQL Server 容錯移轉叢集](../../sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance.md)  
  
  
