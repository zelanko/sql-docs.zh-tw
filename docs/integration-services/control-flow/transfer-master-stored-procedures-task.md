---
title: "傳送主要預存程序工作 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.transfermasterspstask.f1"
helpviewer_keywords: 
  - "傳送主要預存程序工作 [Integration Services]"
ms.assetid: 81702560-48a3-46d1-a469-e41304c7af8e
caps.latest.revision: 25
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 25
---
# 傳送主要預存程序工作
  「傳送主要預存程序」工作會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上的 **master** 資料庫之間，傳送一個或多個使用者自訂預存程序。 若要從 **master** 資料庫傳送預存程序，程序的擁有者必須為 dbo。  
  
 可以設定「傳送主要預存程序」工作傳送所有的預存程序，或只傳送指定的預存程序。 此工作不會複製系統預存程序。  
  
 目的地可能已存在要傳送的主要預存程序。 可以設定「傳送主要預存程序」工作以下列方式處理現有的預存程序：  
  
-   覆寫現有預存程序。  
  
-   存在重複的預存程序時讓工作失敗。  
  
-   略過重複的預存程序。  
  
 在執行階段，「傳送主要預存程序」工作會使用兩個 SMO 連接管理員，連接到來源和目的地伺服器。 SMO 連結管理員會在「傳送主要預存程序」工作以外另行設定，然後在「傳送主要預存程序」工作中參考。 存取伺服器時，SMO 連接管理員會指定要使用的伺服器和驗證模式。 如需相關資訊，請參閱 [SMO Connection Manager](../../integration-services/connection-manager/smo-connection-manager.md)。  
  
## 在 SQL Server 的執行個體之間傳送預存程序  
 「傳送主要預存程序」工作可支援 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 來源及目的地。  
  
## 事件  
 該工作會引發報告已傳送預存程序數目的資訊事件，並在覆寫預存程序時引發警告事件。  
  
 「傳送主要預存程序」工作並不報告登入傳送的累加進度，它只報告 0% 和 100 % 完成。  
  
## 執行值  
 工作之 **ExecutionValue** 屬性中定義的執行值會傳回已傳送的預存程序數。 透過將使用者自訂變數指派給「傳送主要預存程序」工作的 **ExecValueVariable** 屬性，可將與預存程序傳送相關的資訊用於封裝中的其他物件。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 變數](../../integration-services/integration-services-ssis-variables.md)和[在封裝中使用變數](../Topic/Use%20Variables%20in%20Packages.md)。  
  
## 記錄項目  
 「傳送主要預存程序」工作包含下列自訂記錄項目：  
  
-   TransferStoredProceduresTaskStartTransferringObjects  此記錄項目報告傳送已開始。 記錄項目會包含開始時間。  
  
-   TransferSStoredProceduresTaskFinishedTransferringObjects  此記錄項目報告傳送已完成。 記錄項目會包含結束時間。  
  
 此外， **OnInformation** 事件的記錄項目會報告已傳送的預存程序數目，並會為在目的地上覆寫的每個預存程序，寫入 **OnWarning** 事件的記錄項目。  
  
## 安全性和權限  
 使用者必須具有來源上 **master** 資料庫中預存程序清單的檢視權限，且必須是系統管理員 (sysadmin) 伺服器角色的成員，或者具有目的地伺服器上 **master** 資料庫中已建立之預存程序的權限。  
  
## 設定傳送主要預存程序工作  
 您可以透過「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」或以程式設計方式設定屬性。  
  
 如需有關可以在「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」中設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [傳送主要預存程序工作編輯器 &#40;一般頁面&#41;](../../integration-services/control-flow/transfer-master-stored-procedures-task-editor-general-page.md)  
  
-   [傳送主要預存程序工作編輯器 &#40;預存程序頁面&#41;](../../integration-services/control-flow/transfer-master-stored-procedures-task-editor-stored-procedures-page.md)  
  
-   [運算式頁面](../../integration-services/expressions/expressions-page.md)  
  
 如需有關如何以程式設計方式設定這些屬性的詳細資訊，請按以下主題：  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferStoredProceduresTask.TransferStoredProceduresTask>  
  
### 以程式設計方式設定傳送主要預存程序工作  
  
## 相關工作  
 如需有關如何在「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」中設定這些屬性的詳細資訊，請按下列主題：  
  
-   [設定工作或容器的屬性](../Topic/Set%20the%20Properties%20of%20a%20Task%20or%20Container.md)  
  
## 請參閱＜  
 [傳送 SQL Server 物件工作](../../integration-services/control-flow/transfer-sql-server-objects-task.md)   
 [Integration Services 工作](../../integration-services/control-flow/integration-services-tasks.md)   
 [控制流程](../../integration-services/control-flow/control-flow.md)  
  
  