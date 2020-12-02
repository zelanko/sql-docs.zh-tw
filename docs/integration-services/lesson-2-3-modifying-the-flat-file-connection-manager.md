---
description: 課程 2-3：修改一般檔案連線管理員
title: 步驟 3：修改一般檔案連線管理員 | Microsoft Docs
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 459e3995-2116-4f15-aaa2-32f26113869c
author: chugugrace
ms.author: chugu
ms.openlocfilehash: bbe7698c4b97a11fd9b2b4dba581fbad5a8be8df
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "88484102"
---
# <a name="lesson-2-3-modify-the-flat-file-connection-manager"></a>課程 2-3：修改一般檔案連線管理員

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]

在此工作中，您會修改來自第 1 課的「一般檔案」連線管理員。 「一般檔案」連線管理員已設定成以靜態方式載入單一檔案。 若要讓「一般檔案」連線管理員反覆載入檔案，您需將連線管理員的 ConnectionString 屬性變更成使用使用者定義的變數 `User::varFileName`，此變數包含在執行階段要載入的檔案路徑。  
  
透過將連線管理員修改成使用該使用者定義變數的值以變更 ConnectionString 屬性，連線管理員便可連線到不同的一般檔案。 在執行階段，「Foreach 迴圈」容器的每一次反覆運算都會更新 `User::varFileName` 變數。 更新這個變數會造成連接管理員連接到不同的一般檔案，並使資料流程工作處理不同的資料集。  
  
## <a name="configure-the-flat-file-connection-manager-to-use-a-variable"></a>將一般檔案連線管理員設定成使用變數  
  
1.  在 **[連接管理員]** 窗格中，以滑鼠右鍵按一下 **[範例一般檔案來源資料]**，並選取 **[屬性]**。  

2.  在 [屬性] 視窗中確認 **PackagePath** 的開頭為 **\Package.Connections**。 否則，請在 [連線管理員] 窗格中，以滑鼠右鍵按一下 [一般檔案來源資料範例]，並選取 [轉換為套件連線]
  
3.  在 [屬性] 視窗中，針對 [運算式]選取空白資料格，然後選取省略符號按鈕 **(...)**。  
  
4.  在 [屬性運算式編輯器] 對話方塊的 [屬性] 資料行中，選取 [ConnectionString]。  
  
5.  在 [運算式] 資料行中，選取省略符號按鈕 **(…)** 以開啟 [運算式產生器] 對話方塊。  
  
6.  在 [運算式產生器] 對話方塊中，展開 [變數] 節點。  
  
7.  將變數 [User::varFileName] 拖曳至 [運算式] 方塊中。  
  
8.  選取 **[確定]** 以關閉 [運算式產生器] 對話方塊。  
  
9.  再次選取 [確定] 以關閉 [屬性運算式編輯器] 對話方塊。  
  
## <a name="go-to-next-task"></a>移至下一個工作  
[步驟 4：測試第 2 課教學課程套件](../integration-services/lesson-2-4-testing-the-lesson-2-tutorial-package.md)  
  
  
  
