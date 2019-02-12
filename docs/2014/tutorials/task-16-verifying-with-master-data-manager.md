---
title: 工作 16:使用主資料管理員驗證 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 57ad9d3e-8f95-4df6-af01-c291ccf49164
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 3b9e24e062695c3b8b4c1aacd37b464fafd99558
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2019
ms.locfileid: "56023599"
---
# <a name="task-16-verifying-with-master-data-manager"></a>工作 16:使用主資料管理員驗證
  在這項工作中，您會檢查 SSIS 封裝提交的批次作業狀態，並確認資料已使用主資料管理員上傳至 MDS 伺服器。  
  
1.  啟動**主資料管理員**([http://localhost/MDS](http://localhost/MDS))。 如果您已經開啟，請按一下**Microsoft SQL Server Master Data Services**切換至頂端**首頁**。  
  
2.  按一下 **整合管理**。  
  
3.  請注意，有批次包含名為**EIMBatch**您提交在清單中。 按一下 **匯入資料**如果您不會看到下列畫面在功能表列上。  
  
     ![EIM 批次](../../2014/tutorials/media/et-verifyingwithmasterdatamanager.jpg "EIM 批次")  
  
4.  切換回到首頁上，按一下**SQL Server 2012 Master Data Services**頂端。  
  
5.  請確定**供應商**模型選取**模型**並**VERSION_1**選取**版本**，，按一下  **總管**。  
  
6.  您可以看到資料的 SSIS 封裝已匯入至 MDS。 資料應該加以清理，而且沒有重複項目**程式碼**值 (注意：**SupplierID**在 Excel 中的資料行對應至**程式碼**MDS 中 Supplier 實體的屬性)。  
  
## <a name="next-step"></a>下一個步驟  
 [工作 17:檢閱 SSIS 封裝的 DQS 清理專案建立](../../2014/tutorials/task-17-reviewing-dqs-cleansing-project-created-by-the-ssis-package.md)  
  
  
