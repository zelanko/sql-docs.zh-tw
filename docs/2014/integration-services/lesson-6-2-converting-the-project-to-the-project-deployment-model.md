---
title: 步驟 2:將專案轉換為專案部署模型 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 80964293-f1f5-4da7-b1fb-00ab8c30c1c5
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 1ba6dcb7052fed3d209dd87f55789a99df24116c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62767350"
---
# <a name="step-2-converting-the-project-to-the-project-deployment-model"></a>步驟 2:將專案轉換成專案部署模型
  在這個工作中，您將使用 Integration Services 專案轉換精靈，將專案轉換為專案部署模型。  
  
### <a name="converting-the-project-to-the-project-deployment-model"></a>將專案轉換成專案部署模型  
  
1.  在 [專案] 功能表上，按一下 [轉換為專案部署模型]。  
  
2.  在 Integration Services 專案轉換精靈簡介頁面上檢閱步驟，然後按一下 [下一步]。  
  
3.  在 [選取封裝] 頁面上，在封裝清單中，清除 [Lesson 6.dtsx] 以外的所有核取方塊，然後按 [下一步]。  
  
4.  在指定專案屬性頁面上，按一下 [下一步]。  
  
5.  在 [更新執行封裝工作] 頁面上按一下 [下一步]。  
  
6.  在 [選取組態] 頁面上，確定已選取 [設定] 清單中的 Lesson 6.dtsx 封裝，然後按一下 [下一步]。  
  
7.  在 [建立參數] 頁面上確認已在 [組態屬性] 清單中選取 Lesson 6.dtsx 封裝，以及範圍會設定為封裝，然後按一下 [下一步]。  
  
8.  在 [設定參數] 頁面上確認名稱和值的值同於第 5 課中指定變數值和設定值，然後按 [下一步]。  
  
9. 在 [檢閱] 頁面，在 [摘要] 窗格，請注意精靈已經用從組態檔的資訊來設定轉換屬性。  
  
10. 按一下 [轉換]。  
  
     當轉換完成時，會顯示訊息警告不會儲存變更，直到專案儲存在 Visual Studio 中。 在警告對話方塊中按一下 [確定]。  
  
11. 按一下 [Integration Services 專案轉換精靈] 的 [關閉]。  
  
12. 在 SQL Server Data Tools，按一下 [檔案] 功能表，然後按一下 [儲存] 儲存轉換的封裝。  
  
13. 按一下 [參數] 索引標籤，並確認封裝現在包含 VarFolderName 參數，而值的路徑同於從第 5 課組態檔的新範例資料資料夾所指定的路徑。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [步驟 3：測試第 6 課封裝](lesson-6-3-testing-the-lesson-6-package.md)  
  
  
