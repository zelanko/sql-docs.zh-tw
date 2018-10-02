---
title: 偵錯傳遞延伸模組程式碼 | Microsoft Docs
ms.date: 03/16/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: extensions
ms.topic: reference
helpviewer_keywords:
- delivery extensions [Reporting Services], debugging
- debugging delivery extensions [Reporting Services]
- troubleshooting [Reporting Services], delivery extensions
ms.assetid: a7d959da-5005-4a50-aca7-2cef36aa9947
author: markingmyname
ms.author: maghan
ms.openlocfilehash: c6a7bb7b306b3e00d0ed45aa03d42cf4637c4708
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47709035"
---
# <a name="debugging-delivery-extension-code"></a>偵錯傳遞延伸模組程式碼
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 提供數個偵錯工具，可協助您分析傳遞延伸模組程式碼並尋找其中的錯誤。 效果最好的工具將視您嘗試要完成的項目而定。 此範例會使用 [!INCLUDE[vsOrcas](../../../includes/vsorcas-md.md)]。  
  
#### <a name="to-debug-your-delivery-extension-code"></a>偵錯傳遞延伸模組程式碼  
  
1.  啟動 [!INCLUDE[vsOrcas](../../../includes/vsorcas-md.md)]，並開啟您的傳遞延伸模組專案。  
  
2.  建立專案，然後將傳遞延伸模組組件與隨附的 .pdb 檔案，部署到報表伺服器與報表管理員。 如需部署的詳細資訊，請參閱[部署傳遞延伸模組](../../../reporting-services/extensions/delivery-extension/deploying-a-delivery-extension.md)。  
  
3.  如果您已撰寫訂閱使用者介面以擴充報表管理員，請開啟 Internet Explorer 並導覽至報表管理員，同時在 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 中將傳遞延伸模組程式碼保持為開啟的狀態。 如果您沒有為報表管理員部署訂閱使用者介面，請直接開啟用戶端應用程式，並從這個應用程式中，呼叫使用 SOAP API 的傳遞延伸模組。  
  
4.  導覽至 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 與您的傳遞延伸模組專案，並在程式碼中設定某些中斷點。  
  
5.  當傳遞延伸模組專案仍為使用中視窗時，按一下 [偵錯] 功能表的 [附加至處理序]。  
  
     [附加至處理序] 對話方塊隨即開啟。  
  
6.  從處理序清單中，選取 aspnet_wp.exe 處理序 (或者，如果在 IIS 6.0 上部署應用程式則選取 w3wp.exe)，然後按一下 [附加]。  
  
7.  使用您的傳遞延伸模組定義新的訂閱。 您很可能會使用報表管理員或是 SOAP API。 這應該會叫用偵錯工具並執行對應至中斷點的程式碼。  
  
8.  使用 **F11** 鍵逐步執行程式碼。 如需有關使用 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 進行偵錯的詳細資訊，請參閱您的 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 文件集。  
  
## <a name="see-also"></a>另請參閱  
 [實作傳遞延伸模組](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Reporting Services 延伸模組程式庫](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
