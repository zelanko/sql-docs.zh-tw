---
title: "Integration Services 部署精靈 | Microsoft Docs"
ms.custom: ""
ms.date: "08/25/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.ssis.deploymentwizard.f1"
ms.assetid: f3d93e13-2d85-47ff-a913-cda4046491c4
caps.latest.revision: 14
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 14
---
# Integration Services 部署精靈
  [Integration Services 部署精靈] 支援兩種部署模型：
   - 專案部署模型
   - 套件部署模型 
   
 **專案部署模型**可讓您將 SQL Server Integration Services (SSIS) 專案，以單一單位形式部署至 SSIS 目錄。
 
 **套件部署模型**可讓您將已更新的套件部署至 SSIS 目錄，而無須部署整個專案。 
 
 > **注意**：此精靈的預設部署為專案部署模型。  
  
## 啟動精靈
透過下列其中一個方式來啟動精靈：

 - 在 Windows Search 中輸入「SQL Server 部署精靈」 

**OR**

 - 在 SQL Server 安裝資料夾 (例如 C:\Program Files (x86)\Microsoft SQL Server\130\DTS\Binn) 下搜尋可執行檔 **ISDeploymentWizard.exe**。 
 
 > **注意**：若顯示 [簡介] 頁面，請按一下 [下一步] 切換至 [選取來源] 頁面。 
 
 此頁面上的設定視每種部署模型而異。 根據您在此頁面中選取的模型，遵循 [Project Deployment Model](../../integration-services/packages/integration-services-deployment-wizard.md#ProjectModel) 區段或 [Package Deployment Model](../../integration-services/packages/integration-services-deployment-wizard.md#PackageModel) 區段中的步驟執行。  
  
##  <a name="ProjectModel"></a> 專案部署模型  
  
### 選取來源  
 若要部署您建立的專案部署檔案，請選取 [專案部署檔案]  ，並輸入 .ispac 檔案的路徑。 若要部署位於 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中的專案，請選取 **[Integration Services 目錄]**，然後輸入伺服器名稱以及該專案在目錄中的路徑。 按一下 [下一步]  ，以查看 [選取目的地]  頁面。  
  
### 選取目的地  
 若要選取專案在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中的目的地資料夾，請輸入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，或按一下 **[瀏覽]** ，從伺服器清單中選取。 在 SSISDB 中輸入專案路徑，或按一下 **[瀏覽]** 來選取路徑。 按一下 [下一步]  ，以切換至 [檢閱]  頁面。  
  
### 檢閱 (和部署)  
 此頁面可讓您檢閱所選取的設定。 您可以按一下 **[上一步]**，或按一下左窗格中的任何步驟來變更您的選取項目。 按一下 [部署]  開始部署程序。  
  
### 結果  
 完成部署程序之後，您應該會看到 [結果]  頁面。 此頁面會顯示每個動作執行成功或失敗。 如果動作失敗，按一下 **[結果]** 資料行中的 **[失敗]** 以顯示錯誤的說明。 按一下 [儲存結果...]  以將結果儲存至 XML 檔案，或是按一下 [關閉]  結束精靈..  
  
##  <a name="PackageModel"></a> 封裝部署模型  
  
### 選取來源  
 若您選取 [封裝部署]  選項做為 **部署模型** ，則 **Integration Services 部署精靈** 中的 [選取來源] 頁面會顯示封裝部署模型的特定設定。  
  
 若要選取來源封裝，請按一下 [瀏覽...] 按鈕選取包含封裝的**資料夾**，或是在 [封裝資料夾路徑] 文字方塊中輸入資料夾路徑，然後按一下頁面底端的 [重新整理] 按鈕。 現在，您應會於清單方塊中的指定資料夾看見所有封裝。 根據預設，系統會選取所有封裝。 按一下第一個資料行的 **核取方塊** ，選擇您想要部署至伺服器的封裝。  
  
 參閱 [狀態]  和 [訊息]  資料行，以確認封裝的狀態。 若狀態設為 [準備就緒]  或 [警告] ，則部署精靈不會封鎖部署處理程序。 然而，若狀態設為 [錯誤] ，則精靈將不會繼續部署所選的封裝。 若要檢視詳細的警告/錯誤訊息，請按一下 [訊息] 資料行中的連結。  
  
 若使用密碼將敏感性資料或封裝資料加密處理，請在 [密碼]  資料行中輸入密碼，然後按一下 [重新整理]  按鈕確認密碼已獲接受。 若密碼正確，則狀態會變更為 [準備就緒]  ，且警告訊息會消失。 若有多個具相同密碼的封裝，請選取具相同加密密碼的封裝，在 [密碼]  文字方塊中輸入密碼，然後按一下 [套用]  按鈕。 密碼會套用至選取的封裝。  
  
 若所有選取的封裝狀態皆未設定為 [錯誤] ，則會啟用 [下一步]  按鈕讓您得以繼續執行封裝部署處理程序。  
  
### 選取目的地  
 選取封裝來源後，按一下 [下一步]  按鈕切換至 [選取目的地]  頁面。 封裝必須部署至 SSIS 目錄 (SSISDB) 中的專案。 因此在部署封裝前，請確定目的地專案已存在於 SSIS 目錄。 否則會建立空白專案。在 [選取目的地] 頁面的 [伺服器名稱] 文字方塊中輸入伺服器名稱，或是按一下 [瀏覽...] 按鈕選取伺服器執行個體。 按一下 [瀏覽] 按鈕 (在 [路徑] 文字方塊旁)，指定目的地專案。 如果專案不存在，請按一下 [新增專案...] 以建立空白專案做為目的地專案。 專案 **必須** 建立在資料夾下方。  
  
### 檢閱和部署  
 在 [選取目的地]  頁面上，按一下 [下一步]  切換至 **Integration Services 部署精靈** 中的 [檢閱] 頁面。 在檢閱頁面上，檢閱有關部署動作的摘要報告。 驗證完成後，按一下 [部署]  按鈕以執行部署動作。  
  
### 結果  
 部署完成後，您應該會看見 [結果]  頁面。 在 [結果]  頁面中，檢閱部署處理程序中每個步驟的結果。 在 [結果]  頁面上，按一下 [儲存報表]  以儲存部署報表，或是按一下 [關閉]  以關閉精靈。  
  
## 請參閱＜  
 [將專案部署至 Integration Services 伺服器](../../integration-services/packages/deploy-projects-to-integration-services-server.md)   
 [部署專案和封裝](https://msdn.microsoft.com/library/hh213290.aspx)  
  
  