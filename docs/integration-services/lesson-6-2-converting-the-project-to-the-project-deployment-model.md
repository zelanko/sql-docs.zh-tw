---
description: 第 6-2 課：將專案轉換為專案部署模型
title: 步驟 2:將專案轉換為專案部署模型 | Microsoft Docs
ms.custom: ''
ms.date: 01/11/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 80964293-f1f5-4da7-b1fb-00ab8c30c1c5
author: chugugrace
ms.author: chugu
ms.openlocfilehash: fc0e6111542e73ad64a2e82a7f82b3b8bfbf41c4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487742"
---
# <a name="lesson-6-2-convert-the-project-to-the-project-deployment-model"></a>第 6-2 課：將專案轉換為專案部署模型

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]



在此工作中，您會使用 [Integration Services 專案轉換精靈] 將專案轉換為專案部署模型。  
  
1.  在 [專案]**** 功能表上，選取 [轉換為專案部署模型]****。  
  
2.  在 [Integration Services 專案轉換精靈]** 的 [簡介]** **** 頁面上，檢閱步驟，然後選取 [下一步]****。  
  
3.  在 [選取套件]**** 頁面上，清除 [套件]**** 清單中 **Lesson 6.dtsx** 以外的所有核取方塊，然後選取 [下一步]****。  
  
4.  在 [指定專案屬性]**** 頁面上，選取 [下一步]****。  
  
5.  在 [更新執行套件工作]**** 頁面上，選取 [下一步]****。  
  
6.  在 [選取設定]**** 頁面上，確定已選取 [設定]**** 清單中的 **Lesson 6.dtsx** 套件，然後選取 [下一步]****。  
  
7.  在 [建立參數]**** 頁面上，確定已選取 **Lesson 6.dtsx** 套件。  確認 [範圍]**** 是 [設定屬性]**** 清單中的 [套件]****，然後選取 [下一步]****。  
  
8.  在 [設定參數]**** 頁面上，確認 [名稱]**** 和 [值]**** 中的值與第 5 課中為變數和設定值所指定值相同，然後選取 [下一步]****。  
  
9. 在 [檢閱]**** 頁面的 [摘要]**** 窗格中，注意精靈已使用設定檔中的資訊來設定要轉換的 [屬性]****。  
  
10. 選取 [轉換]****。  
  
    轉換完成之後，您會看到警告訊息，指出在您儲存專案之前不會儲存變更。 選取 [確定]**** 以關閉警告對話方塊。  
  
11. 在 [Integration Services 專案轉換精靈]**** 上，選取 [關閉]****。  
  
12. 在 [SQL Server Data Tools]**** 中，選取 [檔案]**** 功能表，然後選取 [儲存]**** 以儲存轉換的套件。  
  
13. 選取 [參數]**** 索引標籤，並確認套件現在包含 **VarFolderName** 的參數。 該參數值是第 5 課設定檔中為 [New Sample Data]**** 資料夾指定的相同路徑。  
  
## <a name="go-to-next-task"></a>移至下一個工作
[步驟 3：測試第 6 課套件](../integration-services/lesson-6-3-testing-the-lesson-6-package.md)  
  
  
  
