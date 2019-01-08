---
title: 來源資料庫檔案 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.transferdatabasetask.sourcedbfiles.f1
ms.assetid: 7dc6bfeb-37c1-45e8-a705-a87564922265
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 42ac066ede8be2af8f08106ed358e63821a92c54
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52533943"
---
# <a name="source-database-files"></a>來源資料庫檔案
  使用 **[來源資料庫檔案]** 對話方塊，即可檢視來源伺服器上的資料庫檔案名稱和位置，或指定傳送資料庫工作的網路檔案共用位置。 如需這項工作的詳細資訊，請參閱 [傳送資料庫工作](control-flow/transfer-database-task.md)。  
  
 若要以來源伺服器上的資料庫檔案名稱和位置來擴展此對話方塊，請在 **[傳送資料庫工作編輯器]** 對話方塊的 **[資料庫]** 頁面中，首先指定 **[SourceConnection]** 和 **[SourceDatabaseName]** 。  
  
## <a name="options"></a>選項。  
 **來源檔案**  
 在來源伺服器上，將會被傳送的資料庫檔案名稱。 **[來源檔案]** 是唯讀的。  
  
 **來源資料夾**  
 在來源伺服器上，要傳送之資料庫檔案所在的資料夾。 **[來源資料夾]** 是唯讀的。  
  
 **網路檔案共用**  
 在來源伺服器上，會從中傳送資料庫檔案的網路共用資料夾。 當您在 **[傳送資料庫工作編輯器]** 對話方塊的 **[資料庫]** 頁面中，將 **[方法]** 指定為 **[DatabaseOffline]** ，以離線模式傳送資料庫時，請使用 **[網路檔案共用]** 。  
  
 輸入網路檔案共用位置，或按一下瀏覽按鈕 **(...)** 以尋找網路檔案共用位置。  
  
 在離線模式中傳送資料庫時，資料庫檔案會複製到來源伺服器上的 **[網路檔案共用]** 位置之後，才傳送到目的地伺服器。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 錯誤和訊息參考](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [傳送資料庫工作編輯器 &#40;一般頁面&#41;](general-page-of-integration-services-designers-options.md)   
 [傳送資料庫工作編輯器 &#40;資料庫頁面&#41;](../../2014/integration-services/transfer-database-task-editor-databases-page.md)  
  
  
