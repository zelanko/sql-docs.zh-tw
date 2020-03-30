---
title: 步驟 1:複製第 1 課套件 | Microsoft Docs
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 7f1616c2-2b4e-4010-be50-27d7b897403a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e73ea716252368e15dcba56242e803d6c1bf93d9
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "71283731"
---
# <a name="lesson-2-1-copy-the-lesson-1-package"></a>課程 2-1：複製第 1 課套件

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



在此工作中，您會建立 **Lesson 1.dtsx**套件的複本。 如果您未完成第 1 課，可以使用本教學課程中所隨附已完成的第 1 課套件。 您將在第 2 課的其餘部分中，全程使用這個新的複本。  
  
## <a name="create-the-lesson-2-package"></a>建立第 2 課套件  

如果您要複製已完成的第 1 課，請使用此程序。  若要複製範例第 1 課，請參閱下一節。
  
1.  如果 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools 尚未開啟，請選取 [開始]   > [所有程式]   > [Microsoft SQL Server 2017]  ，然後選取 [SQL Server Data Tools]  。  
  
2.  在 [檔案]  功能表上，選取 [開啟]   > [專案/方案]  ，選取 [SSIS 教學課程]  資料夾，然後選取 [開啟]  ，再按兩下 [SSIS Tutorial.sln]  。  
  
3.  在 [方案總管]  中，於 [Lesson 1.dtsx]  上按一下滑鼠右鍵，然後選取 [複製]  。  
  
4.  在 [方案總管]  中，於 [SSIS 封裝]  上按一下滑鼠右鍵，然後選取 [貼上]  。  
  
    所複製的套件預設會命名為 **Lesson 2.dtsx**。  
  
5.  在 [方案總管]  中，按兩下 [Lesson 2.dtsx]  以開啟套件  
  
6.  在 [控制流程]  設計介面背景中的任何位置按一下滑鼠右鍵，然後選取 [屬性]  。  
  
7.  在 [屬性]  視窗中，將 [名稱]  屬性變更為**第 2 課**。  
  
8.  依序選取 [識別碼]  屬性的方塊、下拉式箭頭，以及 [\<產生新的識別碼>]  。  
  
## <a name="use-the-sample-lesson-1-package"></a>使用範例第 1 課套件  
  
1.  開啟 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools 及 SSIS 教學課程專案。  
  
2.  在 [方案總管]  中，於 [SSIS 封裝]  上按一下滑鼠右鍵，然後選取 [加入現有的封裝]  。  
  
3.  在 [加入現有封裝的副本]  對話方塊的 [封裝位置]  中，選取 [檔案系統]  。  
  
4.  選取瀏覽 **(…)** 按鈕，瀏覽至您電腦上的 [Lesson 1.dtsx]  ，然後選取 [開啟]  。  
  
5.  複製並貼上第 1 課套件，如上一節中的步驟 3-8 所述。  
  
## <a name="go-to-next-task"></a>移至下一個工作

[步驟 2：新增及設定 Foreach 迴圈容器](../integration-services/lesson-2-2-adding-and-configuring-the-foreach-loop-container.md)  
  
