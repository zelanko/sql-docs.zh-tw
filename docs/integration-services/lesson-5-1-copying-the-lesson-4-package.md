---
title: 步驟 1:複製第 4 課套件 | Microsoft Docs
ms.custom: ''
ms.date: 01/08/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 8aa7d690-4649-4c0a-ac6f-9504637ee426
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 17a72f7d11a2ed743bbede2852b6336ce808a75d
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/26/2019
ms.locfileid: "71295925"
---
# <a name="lesson-5-1-copy-the-lesson-4-package"></a>第 5-1 課：複製第 4 課套件

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



在此工作中，您會建立第 4 課中 **Lesson 4.dtsx** 套件的複本。 如果您並未完成第 4 課，則可將隨附於本教學課程中已完成的第 4 課套件新增至專案，然後建立該套件的複本來使用。 您將在第 5 課的其餘部分中，全程使用這個新的複本。  
  
## <a name="create-the-lesson-5-package"></a>建立第 5 課套件  
  
如果您要複製已完成的第 4 課，請使用此程序。  若要複製範例第 4 課，請參閱下一節。

1.  如果 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools 尚未開啟，請選取 [開始]   > [所有程式]   > [Microsoft SQL Server 2017]  ，然後選取 [SQL Server Data Tools]  。

2.  在 [檔案]  功能表上，選取 [開啟]   > [專案/方案]  ，選取 [SSIS 教學課程]  資料夾，然後選取 [開啟]  。  然後，按兩下 [SSIS Tutorial.sln]  。

3.  在 [方案總管]  中，以滑鼠右鍵按一下 **Lesson 4.dtsx**，然後選取 [複製]  。

4.  在 [方案總管]  中，以滑鼠右鍵按一下 [SSIS 套件]  ，然後選取 [貼上]  。

    所複製套件的名稱預設為 **Lesson 4.dtsx**。

5.  在 [方案總管]  中，按兩下 **Lesson 4.dtsx** 以開啟套件。

6.  在 [控制流程]  設計介面背景中的任何位置按一下滑鼠右鍵，然後選取 [屬性]  。

7.  在 [屬性]  視窗中，將 [名稱]  屬性變更為**第 5 課**。

8.  依序選取 [識別碼]  屬性的方塊、下拉式箭頭，以及 [\<產生新的識別碼>]  。

## <a name="add-the-completed-lesson-4-package"></a>新增已完成的第 4 課套件

1.  開啟 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools 及 SSIS 教學課程專案。

2.  在 [方案總管]  中，於 [SSIS 封裝]  上按一下滑鼠右鍵，然後選取 [加入現有的封裝]  。

3.  在 [加入現有封裝的複本]  對話方塊的 [封裝位置]  中，選取 [檔案系統]  。

4.  選取瀏覽 **(…)** 按鈕，巡覽至您電腦上的 **Lesson 4.dtsx**，然後選取 [開啟]  。

5.  複製並貼上第 4 課套件，如上一節的步驟 3-8 中所述。
  
## <a name="go-to-next-task"></a>移至下一個工作  
[步驟 2：啟用和設定套件設定](../integration-services/lesson-5-2-enabling-and-configuring-package-configurations.md)  
  
