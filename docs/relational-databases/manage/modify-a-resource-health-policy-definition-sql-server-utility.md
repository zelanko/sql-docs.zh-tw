---
title: "修改資源健康情況原則定義 (SQL Server 公用程式) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.SWB.UE.UTILITY.ADMINISTRATION.F1"
ms.assetid: 27bec0b6-92e9-448e-8c70-fe36802cf128
caps.latest.revision: 9
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 9
---
# 修改資源健康情況原則定義 (SQL Server 公用程式)
  此主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 來修改 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的資源健全狀況原則定義。 在您於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式內修改資源使用量原則之前，您必須先建立公用程式控制點 (UCP)。 如需詳細資訊，請參閱 [SQL Server 公用程式的功能與工作](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 您可以針對資料層應用程式和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 受管理的執行個體設定公用程式資源使用率原則。 您可以在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式內針對所有資料層應用程式和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 受管理的執行個體以全域方式定義資源使用率原則，也可以在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式內針對每一個資料層應用程式及每一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 受管理的執行個體個別定義原則。 您也可以實作全域原則，並讓個別的資料層應用程式或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 受管理的執行個體設定自己的原則定義。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### 在 SQL Server 公用程式中修改全域資源使用量原則。  
  
1.  連接到 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中的 UCP。  
  
2.  在 [公用程式總管] 導覽窗格中，按一下 **[公用程式管理]** 來檢視或修改全域監視原則，然後在 [公用程式總管] 內容窗格中按一下 **[原則]** 索引標籤。  
  
3.  在公用程式總管內容窗格中，按一下箭頭或原則描述來選取 [Set global data-tier monitoring policies (設定全域資料層監視原則)] 或 [Set global managed instance monitoring policies (設定全域受管理的執行個體監視原則)]。  
  
4.  您可以使用原則描述右邊的控制項來設定使用量過高或使用量過低原則的臨界值。  
  
5.  視需要使用 [套用] 、[捨棄] 或 [還原預設值]  按鈕。 原則變更最多需要花上 15 分鐘的時間傳回到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式儀表板及清單檢視詳細資料。  
  
6.  若要重新整理資料，請以滑鼠右鍵按一下公用程式總管功能窗格中的 [公用程式管理] 節點，然後選取 [重新整理]。  
  
#### 在 SQL Server 公用程式中，針對個別的資料層應用程式或個別的 SQL Server 受管理的執行個體，修改其資源健全狀況原則定義。  
  
1.  連接到 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中的 UCP。  
  
2.  在公用程式總管功能窗格中，按一下 [部署的資料層應用程式] 或按一下 [受管理的執行個體]，檢視或修改個別資料層應用程式或受管理的執行個體的監視原則。  
  
3.  在公用程式總管內容窗格清單檢視中，按一下您想要修改原則的資料層應用程式或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體名稱，然後按一下 [原則詳細資料] 索引標籤。  
  
4.  按一下箭頭或原則描述，選取要檢視或修改的原則。 預設會選取全域原則。  
  
5.  選取 [覆寫全域原則] 的選項按鈕，針對指定的資料層應用程式來覆寫全域原則及實作個別的原則定義。  
  
6.  您可以使用原則描述右邊的控制項來設定使用量過高或使用量過低原則的臨界值。  
  
7.  視需要使用 [套用] 、[捨棄] 或 [還原預設值]  按鈕。 原則變更最多需要花上 15 分鐘的時間傳回到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式儀表板及清單檢視詳細資料。  
  
8.  若要重新整理資料，請以滑鼠右鍵按一下公用程式總管功能窗格中的 [部署的資料層應用程式] 節點，然後選取 [重新整理]。  
  
## 另請參閱  
 [SQL Server 公用程式的功能與工作](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)   
 [檢視資源健全狀況原則結果 &#40;SQL Server 公用程式&#41;](../../relational-databases/manage/view-resource-health-policy-results-sql-server-utility.md)  
  
  