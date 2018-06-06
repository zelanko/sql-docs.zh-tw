---
title: 移除資料處理延伸模組 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.component: extensions
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- deleting data processing extensions
- data processing extensions [Reporting Services], removing
- removing data processing extensions
ms.assetid: 1d89e32b-0631-44f6-8178-a57fb791d26d
caps.latest.revision: 34
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 01f260e3bb3be11ec878c951470e420fe6156647
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="removing-a-data-processing-extension"></a>移除資料處理延伸模組
  若要移除資料處理延伸模組，請直接從設定檔移除資料處理延伸模組的 **Extension** 項目。 如果您已經為報表伺服器以及報表設計師建立項目，請從 RSReportServer.config 與 RSReportDesigner.config 檔案移除 **Extension** 項目。 在移除組態資訊之後，資料處理延伸模組將無法再供元件使用。  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 延伸模組](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [實作資料處理延伸模組](../../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Reporting Services 延伸模組程式庫](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
