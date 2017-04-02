---
title: "步驟 9：測試第 1 課的教學課程封裝 | Microsoft Docs"
ms.custom: ""
ms.date: "02/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: 9aee7acf-797b-46f2-830d-80ab64a9f0b6
caps.latest.revision: 28
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
---
# 步驟 9：測試第 1 課的教學課程封裝
在這一課，您完成了下列工作：  
  
-   建立新的 [!INCLUDE[ssIS](../includes/ssis-md.md)] 專案。  
  
-   設定封裝要連接到來源和目的地資料時所需的連接管理員。  
  
-   加入資料流程來取得一般檔案來源的資料，對資料執行必要的查閱轉換，以及設定目的地的資料。  
  
現在已完成封裝！ 測試封裝的時間到了。  
  
## 檢查封裝配置  
在測試封裝之前，您應該確認第 1 課封裝中的控制流程和資料流程是否包含下圖所顯示的物件。  
  
**控制流程**  
  
![Control flow in package](../integration-services/media/task9lesson1control.gif "Control flow in package")  
  
**資料流程**  
  
![Data flow in package](../integration-services/media/task9lesson1data.gif "Data flow in package")  
  
### 若要執行第 1 課的教學課程封裝  
  
1.  在 **[偵錯]** 功能表上，按一下 **[開始偵錯]**。  
  
    封裝隨即執行，讓 1097 個資料列順利加入 **AdventureWorksDW2012** 的 **FactCurrency**事實資料表中。  
  
2.  在封裝完成執行之後，在 **[偵錯]** 功能表上，按一下 **[停止偵錯]**。  
  
## 下一課  
[第 2 課：使用 SSIS 新增迴圈](../integration-services/lesson-2-adding-looping-with-ssis.md)  
  
## 另請參閱  
[執行專案和封裝](../Topic/Execution%20of%20Projects%20and%20Packages.md)  
  
  
  
