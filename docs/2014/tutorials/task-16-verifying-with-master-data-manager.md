---
title: 工作16：使用主資料管理員進行驗證 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 57ad9d3e-8f95-4df6-af01-c291ccf49164
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 35dd2da7f6cf6598918cd9d109b97f3d314556d1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "65484694"
---
# <a name="task-16-verifying-with-master-data-manager"></a>工作 16：使用主資料管理員驗證
  在這項工作中，您會檢查 SSIS 封裝提交的批次作業狀態，並確認資料已使用主資料管理員上傳至 MDS 伺服器。  
  
1.  啟動**主資料管理員**（[http://localhost/MDS](http://localhost/MDS)）。 如果已開啟，請按一下頂端的 [ **Microsoft SQL Server Master Data Services** ，切換到**首頁**。  
  
2.  按一下 [**整合管理**]。  
  
3.  請注意，您已在清單中提交名為**EIMBatch**的批次。 如果看不到下列畫面，請按一下功能表列上的 [匯**入資料**]。  
  
     ![EIM 批次](../../2014/tutorials/media/et-verifyingwithmasterdatamanager.jpg "EIM 批次")  
  
4.  按一下頂端的 [ **SQL Server 2012 Master Data Services** ，切換回首頁。  
  
5.  請確定已針對 [**模型**] 選取 [**供應商**型號]，並選取 [**版本**] **VERSION_1** ，然後按一下 [ **Explorer**]。  
  
6.  您可以看到資料的 SSIS 封裝已匯入至 MDS。 資料應該是清理的，而且沒有重複的程式**代碼**值（**注意： Excel**中的 [已加入廠商] 欄對應到 MDS 中供應商實體的**Code**屬性）。  
  
## <a name="next-step"></a>後續步驟  
 [工作 17：檢閱 SSIS 封裝所建立的 DQS 清理專案](../../2014/tutorials/task-17-reviewing-dqs-cleansing-project-created-by-the-ssis-package.md)  
  
  
