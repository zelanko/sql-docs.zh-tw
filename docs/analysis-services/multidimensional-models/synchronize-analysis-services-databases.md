---
title: "同步處理 Analysis Services 資料庫 | Microsoft Docs"
ms.custom: ""
ms.date: "03/06/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Analysis Services 部署, 同步處理資料庫精靈"
  - "部署 [Analysis Services], 同步處理資料庫精靈"
  - "同步處理資料庫精靈"
  - "同步處理 [Analysis Services]"
ms.assetid: 6aeff68d-8470-43fb-a3ed-a4b9685332c2
caps.latest.revision: 40
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 39
---
# 同步處理 Analysis Services 資料庫
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 包含資料庫同步處理功能，此功能藉由將來源伺服器上資料庫的資料和中繼資料複製到目的地伺服器上的資料庫，讓兩個 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫相等。 使用同步處理資料庫功能可完成下列任何一項工作：  
  
-   將資料庫從暫存伺服器部署到實際伺服器。  
  
-   使用暫存伺服器上資料庫的資料和中繼資料變更來更新實際伺服器上的資料庫。  
  
-   產生可在未來執行以同步處理資料庫的 XMLA 指令碼。  
  
-   如果是在多部伺服器上處理 Cube 和維度的分散式工作負載，請使用資料庫同步處理，將變更合併到單一資料庫中。  
  
 資料庫同步處理會在目的地伺服器上起始，將資料和中繼資料提取到來源伺服器上的資料庫複本。 如果資料庫不存在，就會加以建立。 同步處理是單向的一次性作業，一旦資料庫複製之後就會完成。 它並未提供資料庫之間的即時同位檢查。  
  
 您可以重新同步處理已經存在於來源和目的地伺服器上的資料庫，以便將暫存伺服器中的最新變更提取到實際執行資料庫。 系統會比較兩部伺服器上的檔案，看看是否有變更，不同的部分將會予以更新。 在背景進行同步處理時，目的地伺服器上的現有資料庫依然可以使用。 當同步處理正在進行時，使用者可以繼續查詢目的地資料庫。 完成同步處理之後，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會將使用者自動切換到新複製的資料和中繼資料，並卸除目的地資料庫的舊資料。  
  
 若要同步處理資料庫，請執行同步處理資料庫精靈來立即同步處理資料庫，或是用它來產生可於稍後執行的同步處理指令碼。 這兩種方法都可用來提高 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫與 Cube 的可用性和延展性。  
  
> [!NOTE]  
>  以下針對舊版 Analysis Services 所撰寫的技術白皮書依然適用於使用 SQL Server 2012 所建立的可擴充式多維度方案。 如需詳細資訊，請參閱[使用 Analysis Services 向外延展查詢](http://go.microsoft.com/fwlink/?LinkId=253136)和[使用唯讀資料庫向外延展查詢 Analysis Services](http://go.microsoft.com/fwlink/?LinkId=253137.)  
  
## 必要條件  
 在您起始資料庫同步處理的目的地 (或目標) 伺服器上，您必須是 Analysis Services 伺服器管理員角色的成員。 在來源伺服器上，您的 Windows 使用者帳戶必須擁有來源資料庫的完整控制權限。 如果您以互動方式同步處理資料庫，請記得同步處理是在 Windows 使用者識別的安全性內容之下執行。 如果系統拒絕您的帳戶存取特定物件，這些物件將會從作業中排除。 如需伺服器系統管理員角色和資料庫權限的詳細資訊，請參閱[將伺服器系統管理員權限授與 Analysis Services 執行個體](../../analysis-services/instances/grant-server-admin-rights-to-an-analysis-services-instance.md)和[授與資料庫權限 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-database-permissions-analysis-services.md)。  
  
 TCP 通訊埠 2383 必須已在兩部伺服器上開啟，好讓預設執行個體之間能夠進行遠端連接。 如需在 Windows 防火牆中建立例外狀況的詳細資訊，請參閱[設定 Windows 防火牆以允許 Analysis Services 存取](../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)。  
  
 來源伺服器和目的地伺服器必須是相同版本。 每個安裝的版本都必須支援資料庫同步處理。 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中，Enterprise、Developer 和 Business Intelligence 版都支援資料庫同步處理。 如需每版功能的詳細資訊，請參閱 [SQL Server 2016 版本支援的功能](../Topic/Features%20Supported%20by%20the%20Editions%20of%20SQL%20Server%202016.md)。  
  
 每部伺服器上的伺服器部署模式都必須相同。 如果您要同步處理的資料庫是多維度資料庫，則來源和目的地伺服器必須設定多維度伺服器模式。 如需部署模式的詳細資訊，請參閱[判斷 Analysis Services 執行個體的伺服器模式](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)。  
  
 如果您在來源伺服器上使用，請關閉延遲彙總處理。 在背景處理的彙總可能會干擾資料庫同步處理。 如需設定這個伺服器屬性的詳細資訊，請參閱 [OLAP 屬性](../../analysis-services/server-properties/olap-properties.md)。  
  
> [!NOTE]  
>  資料庫大小是判斷同步處理是否為適當方法的一個因素。 我們沒有硬性的規定，但如果同步處理速度太慢，請考慮以平行方式同步處理多部伺服器，如這篇技術文章所述：[Analysis Services 同步處理最佳作法](http://go.microsoft.com/fwlink/?LinkID=253136)。  
  
## 同步處理資料庫精靈  
 使用同步處理資料庫精靈可執行從來源到目的地資料庫的單向同步處理，或是產生指令碼來指定資料庫同步處理作業。 您可以在同步處理過程中同步處理本機和遠端分割區，並選擇是否要包含角色。  
  
 同步處理資料庫精靈會引導您完成下列步驟：  
  
-   選取要同步處理的來源執行個體和資料庫。  
  
-   選取目的地執行個體上之本機分割區的儲存位置。  
  
-   選取其他目的地執行個體上之遠端分割區的儲存位置。  
  
-   選取安全性層級和成員資格的資訊，即可從來源執行個體與資料庫複製到目的地執行個體。  
  
-   選取是否要立即同步處理，還是要將同步處理資料庫精靈所產生的 XML for Analysis (XMLA) [同步處理] 命令儲存到指令碼檔案中，稍後再進行同步處理。  
  
 依預設，除了現有安全性群組中的成員資格之外，精靈會同步處理所有的資料和中繼資料。 同步處理資料和中繼資料時，您可以同時複製所有的安全性設定或忽略所有的安全性設定。  
  
#### 執行精靈  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，連接至執行目的地資料庫的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體。 例如，如果您要將資料庫部署到實際伺服器，您就會在實際伺服器上執行此精靈。  
  
2.  在 [物件總管] 的 [資料庫] 資料夾上按一下滑鼠右鍵，然後按一下 [同步處理]。  
  
3.  指定來源伺服器和來源資料庫。 在 [選取要同步處理的資料庫] 頁面上的 [來源伺服器] 和 [來源資料庫] 中，輸入來源伺服器和來源資料庫的名稱。 例如，如果您要從測試環境部署到實際伺服器，來源就是暫存伺服器上的資料庫。  
  
     [目的地伺服器] 會顯示與資料和中繼資料 (來自 [來源資料庫] 中所選取的資料庫) 同步處理之 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體的名稱。  
  
     名稱相同的來源資料庫與目的地資料庫會發生同步處理。 如果目的地伺服器已經有與來源資料庫共用相同名稱的資料庫，即會以來源的中繼資料和其他資料更新目的地資料庫。 如果資料庫不存在，即會在目的地伺服器上加以建立。  
  
4.  選擇性地變更本機分割區的位置。 使用 [指定本機資料分割的位置] 頁面可指示本機資料分割應該儲存在目的地伺服器上的何處。  
  
    > [!NOTE]  
    >  唯有當至少有一個本機分割區存在於指定的資料庫中時，此頁面才會顯示。  
  
     如果來源伺服器的磁碟機 C 上已安裝分割區集，此精靈可讓您將此分割區集複製到目的地伺服器上的其他位置。 如果您不要變更預設的位置，精靈會將來源伺服器上之每個 Cube 內的量值群組分割區部署到目的地伺服器上的相同位置。 同樣的，如果來源伺服器使用遠端分割區，則目的地伺服器上也會使用相同的遠端分割區。  
  
     [位置] 選項會顯示一個方格，其中列出來源資料夾、目的資料夾，以及要儲存在目的地執行個體上之本機資料分割的預估大小。 此方格包含下列資料行：  
  
     **來源資料夾**  
     顯示來源 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體上，包含本機資料分割的資料夾名稱。 如果資料行包含值「(預設)」，來源執行個體的預設位置就包含本機分割區。  
  
     **目的資料夾**  
     選取目的地 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體上，要與本機資料分割同步處理的資料夾名稱。 如果資料行包含值「(預設)」，目的地執行個體的預設位置就包含本機分割區。  
  
     按一下省略符號 (**...**) 按鈕，來顯示 [瀏覽遠端資料夾] 對話方塊，並指定目的地執行個體上，應與在所選取位置處儲存的本機資料分割同步處理的資料夾。  
  
    > [!NOTE]  
    >  對於在來源執行個體的預設位置處儲存的本機分割區，無法變更此資料行。  
  
     **大小**  
     顯示本機分割區估計的大小。  
  
     [在指定位置的資料分割] 選項會顯示一個方格，其中描述在來源 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體上，在 [位置] 中所選取資料列之 [來源資料夾] 資料行中所指定的位置處，儲存的本機資料分割。  
  
     **Cube**  
     顯示包含分割區之 Cube 的名稱。  
  
     **量值群組**  
     顯示包含分割區之 Cube 中的量值群組的名稱。  
  
     **分割區名稱**  
     顯示分割區的名稱。  
  
     **大小 (MB)**  
     顯示分割區的大小 (以 MB 為單位)。  
  
5.  選擇性地變更遠端資料分割的位置。使用 [指定遠端資料分割的位置] 頁面來指出是否應同步處理來源伺服器上指定之資料庫所管理的遠端資料分割，並且指定應將所選取之遠端資料分割儲存到其中的目的地 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體和資料庫。  
  
    > [!NOTE]  
    >  唯有當至少有一個遠端資料分割是由來源 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體上的指定資料庫所管理時，此頁面才會顯示。  
  
     [位置] 選項會顯示一個方格，其中列出有關來源資料庫之遠端資料分割之儲存位置的詳細資訊，包括來源和目的地資訊，以及各個位置所使用的儲存體大小 (從選取的資料庫取得)。 此方格包含下列資料行：  
  
     **同步處理**  
     選取以納入在同步處理期間包含遠端分割區的位置。  
  
    > [!NOTE]  
    >  如果未針對位置選取此選項，就不會同步處理在該位置處所包含的遠端分割區。  
  
     **來源伺服器**  
     顯示包含遠端分割區之 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體的名稱。  
  
     **來源資料夾**  
     顯示包含遠端分割區之 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體上的資料夾名稱。 如果資料行包含值「(預設)」，[來源伺服器] 中所顯示執行個體的預設位置就包含遠端資料分割。  
  
     **目的地伺服器**  
     顯示 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體的名稱，且應將在 [來源伺服器] 和 [來源資料夾] 中所指定的位置處儲存的遠端資料分割，與此執行個體同步處理。  
  
     按一下省略符號 (**...**) 按鈕，來顯示 [連線管理員] 對話方塊，並指定 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體，且應將在所選取位置處儲存的遠端資料分割，與此執行個體同步處理。  
  
     **目的資料夾**  
     顯示目的地 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體上的資料夾名稱，且要將遠端分割區與此執行個體同步處理。 如果資料行包含值「(預設)」，目的地執行個體的預設位置就應包含遠端分割區。  
  
     按一下省略符號 (**...**) 按鈕，來顯示 [瀏覽遠端資料夾] 對話方塊，並指定目的地執行個體上的資料夾，且應將在所選取位置處儲存的遠端資料分割，與此執行個體同步處理。  
  
     **大小**  
     顯示在此位置處儲存之遠端分割區的估計大小。  
  
     [在指定位置的資料分割] 會顯示一個方格，其中描述在來源 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體上，在 [位置] 中所選取資料列之 [來源資料夾] 資料行中所指定的位置處，儲存的遠端資料分割。 此方格包含下列資料行：  
  
     **Cube**  
     顯示包含分割區之 Cube 的名稱。  
  
     **量值群組**  
     顯示包含分割區之 Cube 中的量值群組的名稱。  
  
     **分割區名稱**  
     顯示分割區的名稱。  
  
     **大小 (MB)**  
     顯示分割區的大小 (以 MB 為單位)。  
  
6.  指定是否應該包含使用者權限資訊以及是否應該使用壓縮。 根據預設，此精靈在將檔案複製到目的地伺服器之前會先壓縮所有資料和中繼資料。 這個選項會產生更快的檔案傳輸速度。 一旦檔案到達目的地伺服器之後，就會解壓縮。  
  
     **全部複製**  
     選取在同步處理期間，要包含安全性定義和成員資格資訊。  
  
     **略過成員資格**  
     選取在同步處理期間，要包含安全性定義，但是排除成員資格資訊。  
  
     **全部忽略**  
     選取此選項可忽略目前位於來源資料庫中的安全性定義和成員資格資訊。 如果在同步處理期間建立目的地資料庫，將不會複製任何安全性定義或成員資格資訊。 如果目的地資料庫已經存在而且有角色和成員資格，將會保留這項安全性資訊。  
  
7.  選擇同步處理方法。 您可以立即同步處理，或是產生儲存至檔案的指令碼。 根據預設，檔案會以 .xmla 副檔名儲存，並且置於 [文件] 資料夾中。  
  
8.  按一下 [完成] 即可同步處理。 在確認 [正在完成精靈] 頁面上的選項之後，再按一下 [完成]。  
  
## 後續步驟  
 如果您並未同步處理角色或成員資格，請記得要指定目的地資料庫目前的使用者存取權限。  
  
## 請參閱＜  
 [Synchronize 元素 &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)   
 [使用 XMLA 部署模型方案](../../analysis-services/multidimensional-models/deploy-model-solutions-using-xmla.md)   
 [Deploy Model Solutions Using the Deployment Wizard](../../analysis-services/multidimensional-models/deploy-model-solutions-using-the-deployment-wizard.md)  
  
  