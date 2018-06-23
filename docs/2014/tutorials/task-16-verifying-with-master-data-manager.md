---
title: 工作 16： 驗證使用主資料管理員 |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 57ad9d3e-8f95-4df6-af01-c291ccf49164
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 36220f21f3e2e28d75ff546857fd87b1e71436f1
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36032206"
---
# <a name="task-16-verifying-with-master-data-manager"></a>工作 16：使用主資料管理員驗證
  在這項工作中，您會檢查 SSIS 封裝提交的批次作業狀態，並確認資料已使用主資料管理員上傳至 MDS 伺服器。  
  
1.  啟動**主資料管理員**([http://localhost/MDS](http://localhost/MDS))。 如果您已經開啟，請按一下**Microsoft SQL Server Master Data Services**在頂端切換到**首頁**。  
  
2.  按一下**整合管理**。  
  
3.  請注意，沒有與批次為**EIMBatch**您提交清單中。 按一下**匯入資料**在功能表列，如果您沒有看到下列畫面。  
  
     ![EIM 批次](../../2014/tutorials/media/et-verifyingwithmasterdatamanager.jpg "EIM 批次")  
  
4.  切換回 [首頁] 頁面按一下**SQL Server 2012 Master Data Services**頂端。  
  
5.  請確定**供應商**模型選取**模型**和**VERSION_1**選取**版本**，然後按一下**總管**。  
  
6.  您可以看到資料的 SSIS 封裝已匯入至 MDS。 資料應該被清理，而且沒有重複項目**程式碼**值 (注意： **SupplierID**在 Excel 中的資料行對應至**程式碼**MDS 中 Supplier 實體的屬性)。  
  
## <a name="next-step"></a>下一個步驟  
 [工作 17： 檢閱 DQS 清理專案所建立的 SSIS 封裝](../../2014/tutorials/task-17-reviewing-dqs-cleansing-project-created-by-the-ssis-package.md)  
  
  