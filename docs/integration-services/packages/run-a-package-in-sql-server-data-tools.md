---
title: "在 SQL Server Data Tools 中執行封裝 | Microsoft Docs"
ms.custom: ""
ms.date: "08/25/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Integration Services 封裝, 執行"
  - "SSIS 封裝, 執行"
  - "封裝 [Integration Services]，執行"
  - "SQL Server Integration Services 封裝, 執行"
ms.assetid: 318e6beb-5540-4101-82a5-18c9d47f0570
caps.latest.revision: 58
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 58
---
# 在 SQL Server Data Tools 中執行封裝
  在開發、偵錯和測試封裝期間，您通常會在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中執行封裝。 當您從「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」執行封裝時，封裝一定會立即執行。  
  
 封裝執行時， [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師會在 **[進度]** 索引標籤上顯示封裝執行的進度。 您可以檢視封裝的開始和結束時間、它的工作和容器，以及封裝中任何失敗之工作或容器的相關資訊。 在完成執行封裝後，執行階段資訊會在 [執行結果] 索引標籤上保持可用。 如需詳細資訊，請參閱＜ [Debugging Control Flow](../../integration-services/troubleshooting/debugging-control-flow.md)＞主題中的＜進度報表＞一節。  
  
 **設計階段部署**。 當您在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中執行封裝時，會建立封裝，然後部署至資料夾。 在執行封裝之前，您可以指定要用來部署封裝的資料夾。 如果未指定資料夾，預設將會使用 **bin** 資料夾。 這種類型的部署稱為設計階段部署。  
  
### 若要在 SQL Server Data Tools 中執行封裝  
  
1.  在方案總管中，如果您的方案包含多個專案，請以滑鼠右鍵按一下包含封裝的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案，然後按一下 [設定為啟始物件] 以設定啟始物件。  
  
2.  在方案總管中，如果您的專案包含多個封裝，請以滑鼠右鍵按一下封裝，然後按一下 [設定為啟始物件] 以設定啟始封裝。  
  
3.  若要執行封裝，請使用下列其中一個程序：  
  
    -   開啟您要執行的封裝，然後按一下功能表列上的 **[啟動偵錯]** ，或按下 F5。 在封裝完成執行後，按下 Shift+F5 以返回設計模式。  
  
    -   在方案總管中，以滑鼠右鍵按一下封裝，然後按一下 [執行封裝]。  
  
### 若要為設計階段部署指定不同的資料夾  
  
1.  在方案總管中，以滑鼠右鍵按一下包含您要執行之封裝的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案資料夾，然後按一下 [屬性]。  
  
2.  在 [\<專案名稱> 屬性頁] 對話方塊中，按一下 [建立]。  
  
3.  更新 OutputPath 屬性中的值，以指定要用於設計階段部署的資料夾，然後按一下 [確定]。  
  
## 請參閱＜  
 [執行專案和封裝](https://msdn.microsoft.com/library/hh213290.aspx)   
 [Integration Services (SSIS) 封裝](https://msdn.microsoft.com/library/ms141134.aspx)  
  
  