---
title: 上傳檔案到資料夾 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- publishing reports [Reporting Services], uploading files
- reports [Reporting Services], publishing
- uploading reports [Reporting Services]
- uploading files [Reporting Services]
- files [Reporting Services], uploading
- files [Reporting Services]
- folders [Reporting Services], uploading files to
ms.assetid: 2f99a288-d4aa-4c64-b310-e457a2aef2c5
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 341a5ca0a25729acbf38e961f714f13aedc0dfd4
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2019
ms.locfileid: "56031201"
---
# <a name="upload-files-to-a-folder"></a>上傳檔案到資料夾
  您可以從檔案系統上傳檔案，並將其當成 Managed 項目儲存在報表伺服器資料庫中。 上傳檔案會有何狀況取決於檔案類型。  
  
-   上傳 .rdl 檔案相當於發行報表。  
  
-   上傳任何其他檔案，會將檔案當做單一的二進位物件加入到報表伺服器資料庫中。 這些檔案會發行至報表伺服器做為資源。 資源可以是任何檔案類型。 如果副檔名符合已知的 MIME 類型，則會使用 MIME 類型的圖示來識別資源類型。 否則，會以一般檔案圖示表示資源。  
  
> [!NOTE]  
>  您不能上傳報表資料來源 (.rds) 檔案，以建立共用資料來源。 .rds 檔案只能在報表設計師中使用。 它無法提供您透過報表管理員定義與管理之共用資料來源項目的內容。 上傳的替代方法，是撰寫指令碼來建立以 .rds 檔案為基礎的共用資料來源。  
  
 上傳項目的檔案大小上限是由 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)]所決定。 根據預設，大小上限是 4 MB。  
  
 您上傳至報表伺服器資料庫的檔案，在資料夾階層中會使用下列圖示進行視覺化表示。  
  
 ![報表圖示](../media/hlp-16doc.gif "報表圖示")  
報表圖示  
  
 ![模型圖示](../media/model-icon.gif "模型圖示")  
報表模型圖示  
  
 ![一般資源圖示](../media/hlp-16file.gif "一般資源圖示")  
一般資源圖示  
  
 上傳檔案時，檔案永遠會放在目前所選取的資料夾中。 您可以先導覽至要包含項目的資料夾，或是上傳檔案然後再移動到最終位置。  
  
 若要上傳檔案，請使用報表管理員。 您是否能夠上傳檔案到報表伺服器，是依您角色指派中的工作而定。 如果您使用預設安全性，本機管理員就可以將項目加入報表伺服器。 如果已啟用我的報表，則只要是有 [我的報表] 資料夾的使用者，都有權將項目上傳至該資料夾。 如果您使用自訂角色指派，角色指派就必須包括支援資料夾管理的工作。  
  
|動作|包括下列工作|  
|----------------|-------------------------|  
|將 .rdl 檔案上傳至資料夾|管理報表|  
|將任何檔案當成二進位物件上傳|管理資源|  
|檢視資料夾的內容|檢視資源、檢視報表|  
  
## <a name="see-also"></a>另請參閱  
 [報表管理員&#40;SSRS 原生模式&#41;].../ 報表-manager-ssrs-原生-mode.md）   
 [在原生模式報表伺服器上授與權限](../security/granting-permissions-on-a-native-mode-report-server.md)   
 [工作和權限](../security/tasks-and-permissions.md)   
 [上傳檔案或報表 &#40;報表管理員&#41;](../reports/upload-a-file-or-report-report-manager.md)  
  
  
