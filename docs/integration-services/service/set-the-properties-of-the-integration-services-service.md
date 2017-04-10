---
title: "設定 Integration Services 服務的屬性 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Integration Services 服務, 設定"
  - "Integration Services 服務, 屬性"
ms.assetid: 3a8ad546-0f58-4b31-ab56-58d6313b1098
caps.latest.revision: 31
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 31
---
# 設定 Integration Services 服務的屬性
    
> [!IMPORTANT]  
>  本主題會討論 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務，即用於管理 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝的 Windows 服務。 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 支援此服務能與舊版 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]回溯相容。 從 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]開始，您可以管理 Integration Services 伺服器上的物件，例如封裝。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務會管理並監視 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的封裝。 當您首次安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]時， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務就會啟動，而且此服務的啟動類型會設定為自動。  
  
 在您已經安裝 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務之後，就可以使用 [SQL Server 組態管理員] 或 [服務] MMC 嵌入式管理單元來設定服務的屬性。  
  
 若要設定服務的其他重要功能 (包括它儲存和管理封裝的位置)，您就必須修改服務的組態檔。 如需詳細資訊，請參閱[設定 Integration Services 服務 &#40;SSIS 服務&#41;](../../integration-services/service/configuring-the-integration-services-service-ssis-service.md)。  
  
### 使用 SQL Server 組態管理員來設定 Integration Services 服務的屬性  
  
1.  在 **[開始]** 功能表上，依序指向 **[所有程式]**、 **[Microsoft SQL Server]**和 **[組態工具]**，然後按一下 **[SQL Server 組態管理員]**。  
  
2.  在 [SQL Server 組態管理員] 嵌入式管理單元中，尋找服務清單中的 [SQL Server Integration Services]，以滑鼠右鍵按一下 [SQL Server Integration Services]，然後按一下 [屬性]。  
  
3.  在 **[SQL Server Integration Services 屬性]** 對話方塊中，可以執行下列操作：  
  
    -   按一下 **[登入]** 索引標籤，以檢視登入資訊 (例如帳戶名稱)。  
  
    -   按一下 **[服務]** 索引標籤，即可檢視服務的相關資訊 (例如主機電腦的名稱)，並指定 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務的啟動模式。  
  
        > [!NOTE]  
        >  [進階] 索引標籤不包含 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務的資訊。  
  
4.  按一下 **[確定]**。  
  
5.  在 [檔案] 功能表上，按一下 [結束]，以關閉 [SQL Server 組態管理員] 嵌入式管理單元。  
  
### 使用服務來設定 Integration Services 服務的屬性  
  
1.  在 **[控制台]**中，如果您使用「一般檢視」，請按一下 **[系統管理工具]**，如果您使用「類別檢視」，請按一下 **[效能及維護]** ，然後按一下 **[系統管理工具]**。  
  
2.  按一下 **[服務]**。  
  
3.  在 [服務] 嵌入式管理單元中，尋找服務清單中的 [SQL Server Integration Services]，以滑鼠右鍵按一下 [SQL Server Integration Services]，然後按一下 [屬性]。  
  
4.  在 **[SQL Server Integration Services 屬性]** 對話方塊中，您可以執行下列動作：  
  
    -   按一下 **[一般]** 索引標籤。 若要啟用服務，請選取手動或自動啟動類型。 若要停用服務，請在 **[啟動類型]** 方塊中選取 [停用]。 選取 [停用] 不會停止目前正在執行的服務。  
  
         如果已啟用服務，則可以按一下 **[停止]** 停止服務，或按一下 **[啟動]** 啟動服務。  
  
    -   按一下 **[登入]** 索引標籤，即可檢視或編輯登入資訊。  
  
    -   按一下 **[復原]** 索引標籤，以檢視服務失敗的預設電腦回應。 您可以修改這些選項，以配合您的環境。  
  
    -   按一下 **[相依性]** 索引標籤，以檢視相依性服務的清單。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務不具有相依性。  
  
5.  按一下 **[確定]**。  
  
6.  或者，如果啟動類型是 [手動] 或 [自動]，則可以用滑鼠右鍵按一下 [SQL Server Integration Services]，然後按一下 [啟動]、[停止] 或 [重新啟動]。  
  
7.  在 [檔案] 功能表上，按一下 [結束]，以關閉 [服務] 嵌入式管理單元。  
  
## 請參閱＜  
 [管理 Integration Services 服務](../../integration-services/service/manage-the-integration-services-service.md)  
  
  