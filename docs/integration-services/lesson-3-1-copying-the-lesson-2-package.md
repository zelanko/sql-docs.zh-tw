---
title: 步驟 1:複製第 2 課套件 | Microsoft Docs
ms.custom: ''
ms.date: 01/04/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 4bd91402-4e37-41de-ab78-8ca5a1948a37
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 75a1cd07710bb95c041d0de8a00cb23f7354eb91
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/16/2019
ms.locfileid: "65722398"
---
# <a name="lesson-3-1-copy-the-lesson-2-package"></a>課程 3-1：複製第 2 課套件

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



在此工作中，您會從第 2 課的 Lesson 2.dtsx 套件建立一個複本。 如果您未完成第 2 課，可以將本教學課程中所隨附已完成的第 2 課套件新增到專案中，然後改為複製該套件。 您將在第 3 課的其餘部分中，全程使用這個新的複本。

## <a name="create-the-lesson-3-package"></a>建立第 3 課套件

如果您要複製已完成的第 2 課，請使用此程序。  若要複製範例第 2 課，請參閱下一節。

1.  如果 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools 尚未開啟，請選取 [開始] > [所有程式] > [Microsoft SQL Server 2017]，然後選取 [SQL Server Data Tools]。

2.  在 [檔案] 功能表上，選取 [開啟] > [專案/方案]，選取 [SSIS 教學課程] 資料夾，然後選取 [開啟]，再按兩下 [SSIS Tutorial.sln]。

3.  在 [方案總管] 中，於 [Lesson 2.dtsx] 上按一下滑鼠右鍵，然後選取 [複製]。

4.  在 [方案總管] 中，於 [SSIS 封裝] 上按一下滑鼠右鍵，然後選取 [貼上]。

    所複製套件的名稱預設為 Lesson 3.dtsx。

5.  在 [方案總管] 中，按兩下 [Lesson 3.dtsx] 以開啟套件

6.  在 [控制流程] 設計介面背景中的任何位置按一下滑鼠右鍵，然後選取 [屬性]。

7.  在 [屬性] 視窗中，將 [名稱] 屬性變更為**第 3 課**。

8.  依序選取 [識別碼] 屬性的方塊、下拉式箭頭，以及 [\<產生新的識別碼>]。

## <a name="add-the-completed-lesson-2-package"></a>新增已完成的第 2 課套件

1.  開啟 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools 及 SSIS 教學課程專案。

2.  在 [方案總管] 中，於 [SSIS 封裝] 上按一下滑鼠右鍵，然後選取 [加入現有的封裝]。

3.  在 [加入現有封裝的副本] 對話方塊的 [封裝位置] 中，選取 [檔案系統]。

4.  選取瀏覽 **(…)** 按鈕，瀏覽至您機器上的 [Lesson 2.dtsx]，然後選取 [開啟]。

5.  複製並貼上第 3 課套件，如上一節中的步驟 3-8 所述。  
  
## <a name="go-to-next-task"></a>移至下一個工作
[步驟 2：新增及設定記錄](../integration-services/lesson-3-2-adding-and-configuring-logging.md)  
  
