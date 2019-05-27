---
title: 目的地資料庫檔案 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.transferdatabasetask.destdbfiles.f1
ms.assetid: f6f90417-86fb-4b8c-a790-0b215c344ef6
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2cfee31b4167625b4f868d7312abd752a215652c
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66059550"
---
# <a name="destination-database-files"></a>目的地資料庫檔案
  使用 **[目的地資料庫檔案]** 對話方塊，即可檢視或變更目的地伺服器上的資料庫檔案名稱和位置，或是指定傳送資料庫工作的網路檔案位置。 如需這項工作的詳細資訊，請參閱 [傳送資料庫工作](control-flow/transfer-database-task.md)。  
  
 若要使用來源伺服器上的資料庫檔案名稱和位置，來自動擴展此對話方塊，請先在 **[傳送資料庫工作編輯器]** 對話方塊的 **[資料庫]** 頁面中，指定 **[SourceConnection]** 、 **[SourceDatabaseName]** 和 **[SourceDatabaseFiles]** 。  
  
## <a name="options"></a>選項  
 **目的地檔案**  
 目的地伺服器上已傳送資料庫檔案的名稱。  
  
 輸入檔案名稱，或是按一下檔案名稱來編輯它。  
  
 **目的資料夾**  
 目的地伺服器上的資料夾，用於存放將傳送的資料庫檔案。  
  
 輸入資料夾路徑，按一下該資料夾路徑來編輯它，或是按一下瀏覽來找出在目的地伺服器上的資料夾，以存放要傳送的資料庫檔案。  
  
 **網路檔案共用**  
 在目的地伺服器上的網路共用資料夾，其中存放要傳送的資料庫檔案。 當您在 **[傳送資料庫工作編輯器]** 對話方塊的 **[資料庫]** 頁面中，將 **[方法]** 指定為 **[DatabaseOffline]** ，以離線模式傳送資料庫時，請使用 **[網路檔案共用]** 。  
  
 輸入網路檔案共用位置，或是按一下瀏覽來找出網路檔案共用位置。  
  
 當您以離線模式傳送資料庫時，在將資料庫檔案傳送到 **[目的資料夾]** 位置之前，會將其複製到 **[網路檔案共用]** 位置。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 錯誤和訊息參考](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [傳送資料庫工作編輯器 &#40;一般頁面&#41;](general-page-of-integration-services-designers-options.md)   
 [傳送資料庫工作編輯器 &#40;資料庫頁面&#41;](../../2014/integration-services/transfer-database-task-editor-databases-page.md)  
  
  
