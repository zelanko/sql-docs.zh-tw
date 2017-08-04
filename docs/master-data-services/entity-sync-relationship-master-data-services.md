---
title: "實體同步關係 (Master Data Services) |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: bd627a2d-dc64-47e9-9a71-2d0ad04b4962
caps.latest.revision: 6
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1b0b6276a63b50e327879b6bbfff1a235349cdaf
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="entity-sync-relationship-master-data-services"></a>實體同步關聯性 (Master Data Services)
  實體同步是實體版本間單向且可重複的同步處理。 它可讓您在不同模型間共用實體資料。 您可以將事實的單一來源保留在一個模型，並且在其他模型中重複使用此主要資料。 例如，您可以將美國的狀態資料儲存在一個模型實體，並且在其他模型中重複使用該資料。  
  
 實體同步時，您也可以進行資料的一次性複製。  
  
 來源實體中具有任意格式和檔案屬性的所有分葉成員，都會在同步執行期間同步處理至目標實體。 這會建立、刪除和修改實體結構描述和成員。  
  
 一旦建立同步關聯性，目標實體只能由同步處理程序修改。 隨時可以移除同步關聯性，讓目標實體可供編輯。  
  
## <a name="see-also"></a>另請參閱  
 [建立及執行實體同步關係 &#40;Master Data Services&#41;](../master-data-services/create-and-execute-an-entity-sync-relationship-master-data-services.md)   
 [編輯和刪除實體同步關係 &#40;Master Data Services&#41;](../master-data-services/edit-and-delete-an-entity-sync-relationship-master-data-services.md)  
  
  
