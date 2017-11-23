---
title: "建立及管理遠端資料分割 (Analysis Services) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- partitions [Analysis Services], remote
- remote partitions [Analysis Services]
ms.assetid: 4322b5cb-af07-4e79-8ecb-59e1121a9eb8
caps.latest.revision: "30"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: bbcff2fe14716ebb2af74430538573706f8c2475
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="create-and-manage-a-remote-partition-analysis-services"></a>建立及管理遠端分割區 (Analysis Services)
  分割量值群組時，您可以在遠端 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體上設定次要資料庫作為分割區儲存。  
  
 Cube (稱為 master 資料庫) 的遠端分割區，會儲存在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 遠端執行個體上的專用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫 (稱為次要資料庫) 中。  
  
 專用次要資料庫會針對唯一的 master 資料庫儲存遠端資料分割，但是 master 資料庫可以使用多個次要資料庫，只要所有次要資料庫都在相同的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]遠端執行個體上即可。 資料庫中專屬於遠端分割區的維度會建立為連結維度。  
  
## <a name="prerequisites"></a>必要條件  
 建立遠端分割區之前，必須先符合下列條件：  
  
-   您必須具有次要 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體和專用資料庫以儲存資料分割。 次要資料庫的用途只有一個，那就是為 master 資料庫提供遠端分割區儲存。  
  
-   這兩個伺服器執行個體的版本必須相同。 這兩個資料庫應該是相同的功能層級。  
  
-   這兩個執行個體必須設定 TCP 連接。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 不支援使用 HTTP 通訊協定建立遠端資料分割。  
  
-   這兩部電腦上的防火牆設定必須設為接受外部連接。 如需設定防火牆的資訊，請參閱 [設定 Windows 防火牆以允許 Analysis Services 存取](../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)。  
  
-   執行 master 資料庫之執行個體的服務帳戶必須具有 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]遠端執行個體的管理存取權限。 如果服務帳戶變更，您必須更新伺服器和資料庫上的權限。  
  
-   您必須是兩部電腦的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 管理員。  
  
-   您必須確保災害復原計畫包含遠端分割區的備份與還原。 使用遠端分割區會讓備份與還原作業變得很複雜。 請務必針對您的計畫進行徹底的測試，確保能夠還原必要資料。  
  
## <a name="configure-remote-partitions"></a>設定遠端分割區  
 執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體的兩部不同電腦都必須建立遠端資料分割配置，其中一部電腦指定為主要伺服器，而另一部電腦指定為從屬伺服器。  
  
 下列程序假設您有兩個伺服器執行個體，其中 Cube 資料庫部署在主要伺服器上。 基於此程序的目的，Cube 資料庫稱為 db-master。 包含遠端分割區的儲存資料庫稱為 db-storage。  
  
 您將使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 和 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 完成此程序。  
  
> [!NOTE]  
>  遠端分割區只能與其他遠端分割區合併。 如果使用本機和遠端分割區的組合，替代方式是建立包含合併資料的新分割區，並刪除您不再使用的分割區。  
  
#### <a name="specify-valid-server-names-for-cube-deployment-in-ssdt"></a>為 Cube 部署指定有效的伺服器名稱 (在 SSDT 中)  
  
1.  在主要伺服器上：在方案總管中，以滑鼠右鍵按一下方案名稱，然後選取 [屬性]。 在 [屬性] 對話方塊中，依序按一下 [組態屬性]、[部署] 及 [伺服器]，然後設定主要伺服器的名稱。  
  
2.  在從屬伺服器上：在方案總管中，以滑鼠右鍵按一下方案名稱，然後選取 [屬性]。 在 [屬性] 對話方塊中，依序按一下 [組態屬性]、[部署] 及 [伺服器]，然後設定從屬伺服器的名稱。  
  
#### <a name="create-and-deploy-a-secondary-database-in-ssdt"></a>建立及部署次要資料庫 (在 SSDT 中)  
  
1.  在從屬伺服器上：為儲存資料庫建立新的 Analysis Services 專案。  
  
2.  在從屬伺服器上：在 [方案總管] 中，建立指向 Cube 資料庫 (db-master) 的新資料來源。 使用提供者 **Native OLE DB\Microsoft OLE DB Provider for Analysis Services 11.0**。  
  
3.  在從屬伺服器上：部署方案。  
  
#### <a name="enable-features-in-ssms"></a>啟用功能 (在 SSMS 中)  
  
1.  在從屬伺服器上：在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，以滑鼠右鍵按一下物件總管中已連接的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體，然後選取 [屬性]。 將 **Feature\LinkToOtherInstanceEnabled** 和 **Feature\LinkFromOtherInstanceEnabled** 設為 **True**。  
  
2.  在從屬伺服器上：以滑鼠右鍵按一下物件總管中的伺服器名稱，然後選取 [重新啟動] 以重新啟動伺服器。  
  
3.  在主要伺服器上：在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，以滑鼠右鍵按一下物件總管中已連接的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體，然後選取 [屬性]。 將 **Feature\LinkToOtherInstanceEnabled** 和 **Feature\LinkFromOtherInstanceEnabled** 設為 **True**。  
  
4.  在主要伺服器上：若要重新啟動伺服器，請以滑鼠右鍵按一下物件總管中的伺服器名稱，然後選取 [重新啟動]。  
  
#### <a name="set-the-masterdatasourceid-database-property-on-the-remote-server-in-ssms"></a>設定遠端伺服器上的 MasterDataSourceID 資料庫屬性 (在 SSMS 中)  
  
1.  在從屬伺服器上：在儲存資料庫 (db-storage) 上按一下滑鼠右鍵，並指向 [編寫資料庫的指令碼為] | [ALTER 至] | [新增查詢編輯器視窗]。  
  
2.  將 **MasterDataSourceID** 加入 XMLA 中，然後指定 Cube 資料庫 db-master 的識別碼作為其值。 XMLA 看起來應該類似如下。  
  
    ```  
    <Alter ObjectExpansion="ExpandFull" xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
    <Object>  
       <DatabaseID>DB-Storage</DatabaseID>  
    </Object>  
    <ObjectDefinition>  
       <Database xmlns:xsd="http://www.w3.org/2001/XMLSchema" 400"   
          <ID>DB-Storage</ID>  
          <Name>DB-StorageB</Name>  
          <ddl200:CompatibilityLevel>1100</ddl200:CompatibilityLevel>  
          <Language>1033</Language>  
          <Collation>Latin1_General_CI_AS</Collation>  
          <DataSourceImpersonationInfo>  
    <ImpersonationMode>ImpersonateAccount</ImpersonationMode>  
             <Account>*********</Account>  
          </DataSourceImpersonationInfo>  
          <MasterDataSourceID>DB-Master</MasterDataSourceID>  
       </Database>  
    </ObjectDefinition>  
    </Alter>  
    ```  
  
3.  按 F5 執行指令碼。  
  
#### <a name="set-up-the-remote-partition-in-ssdt"></a>設定遠端分割區 (在 SSDT 中)  
  
1.  在主要伺服器上：開啟 Cube 設計師中的 Cube，然後按一下 [資料分割] 索引標籤。展開量值群組。 如果為多個資料分割設定量值群組，請按一下 [新增資料分割]；否則在 [來源] 資料行中按一下瀏覽 (. 。 ) 按鈕，以編輯現有的分割區。  
  
2.  在 [資料分割精靈] 的 [指定來源資訊] 中，選取原始資料來源檢視和事實資料表。  
  
3.  如果使用查詢繫結，請為建立的新分割區提供分割資料的 WHERE 子句。  
  
4.  在 [處理與儲存位置] 的 [處理位置] 下，選擇 [遠端 Analysis Services 資料來源]，然後按一下 [新增]，以建立指向從屬資料庫 db-storage 的新資料來源。  
  
    > [!NOTE]  
    >  如果發生錯誤，指出集合中不存在此資料來源，您必須開啟儲存資料庫 db-storage 的專案，然後建立指向 master 資料庫 db-master 的資料來源。  
  
5.  在主要伺服器上：以滑鼠右鍵按一下方案總管中的 Cube 名稱，然後選取 [處理] 並完整處理 Cube。  
  
## <a name="administering-remote-partitions"></a>管理遠端分割區  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 支援遠端資料分割的平行和循序處理。 定義分割區的 master 資料庫會協調參與處理 Cube 之分割區所有執行個體之間的交易。 然後將處理報表傳送至處理分割區的所有執行個體。  
  
 您可以在單一 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]執行個體上同時管理內含遠端分割區的 Cube 及其分割區。 但是，您只能在定義遠端分割區及其父 Cube 的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體上，檢視及更新分割區的中繼資料。 您無法在遠端 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]執行個體上，檢視或更新遠端資料分割。  
  
> [!NOTE]  
>  雖然結構描述資料列集不會顯示專用於儲存遠端分割區的資料庫，但是使用分析管理物件 (AMO) 的應用程式仍可使用 XML for Analysis Discover 命令探索專用資料庫。 任何使用 TCP 或 HTTP 用戶端直接傳送至專用資料庫的 CREATE 或 DELETE 命令會成功完成，但是伺服器會傳回警告，指出這些動作可能會損毀此密切管理的資料庫。  
  
## <a name="see-also"></a>請參閱＜  
 [資料分割 &#40;Analysis Services - 多維度資料&#41;](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)  
  
  
