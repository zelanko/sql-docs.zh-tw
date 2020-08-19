---
description: 課程 1-2 - 建立部署專案
title: 步驟 2：建立部署專案 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 59990fe2-7036-4e9c-8efc-6ece9e66eda7
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 025e601dfb6f062246d1edcb1799c1daf2b69886
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449669"
---
# <a name="lesson-1-2---creating-the-deployment-project"></a>課程 1-2 - 建立部署專案

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]


在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]中，可部署的單位是 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案。 部署封裝之前，必須先建立新的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案，並且將所有封裝以及要隨同封裝一起部署的所有輔助檔案全部加入至該專案中。  
  
### <a name="to-create-the-integration-services-project"></a>若要建立 Integration Services 專案  
  
1.  按一下 [開始]****，依序指向 [所有程式]**** 和 [Microsoft SQL Server]****，然後按一下 [SQL Server]、[SQL Server Data Tools]****。  
  
2.  在 [檔案]**** 功能表上，指向 [開新檔案]****，然後按一下 [專案]**** 建立新的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案。  
  
3.  在 [新增專案]**** 對話方塊中，選取 [範本]**** 窗格中的 [Integration Services 專案]****。  
  
4.  在 [名稱]**** 方塊中，將預設名稱變更為**部署教學課程**。 您可以選擇性地清除 **[建立方案的目錄]** 核取方塊。  
  
5.  接受預設位置，或按一下 [瀏覽]**** 尋找您要使用的資料夾。  
  
6.  在 [專案位置]**** 對話方塊中，按一下該資料夾，然後按一下 [開啟]****。  
  
7.  按一下 [確定]  。  
  
8.  依預設，會建立名稱為 Package.dtsx 的空白封裝，並將其加入至專案中。 但是，您並不會使用此封裝，而是將現有的封裝加入至專案中。 由於專案中的所有封裝都會包含在部署中，因此應該刪除 Package.dtsx。 若要刪除，請以滑鼠右鍵按一下這個檔案，然後按一下 [刪除]****。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
[步驟 3：新增封裝和其他檔案](../integration-services/lesson-1-3-adding-packages-and-other-files.md)  
  
## <a name="see-also"></a>另請參閱  
[Integration Services &#40;SSIS&#41; 專案](~/integration-services/integration-services-ssis-projects-and-solutions.md)  
  
  
  

