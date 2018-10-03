---
title: 移除資料處理延伸模組 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.topic: reference
helpviewer_keywords:
- deleting data processing extensions
- data processing extensions [Reporting Services], removing
- removing data processing extensions
ms.assetid: 1d89e32b-0631-44f6-8178-a57fb791d26d
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 7a1ad001df3353d4f114ec5ef38af2a7fdc9f142
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48200048"
---
# <a name="removing-a-data-processing-extension"></a>移除資料處理延伸模組
  若要移除資料處理延伸模組，請直接從設定檔移除資料處理延伸模組的 **Extension** 項目。 如果您已經為報表伺服器以及報表設計師建立項目，請從 RSReportServer.config 與 RSReportDesigner.config 檔案移除 **Extension** 項目。 在移除組態資訊之後，資料處理延伸模組將無法再供元件使用。  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 延伸模組](../reporting-services-extensions.md)   
 [實作資料處理延伸模組](implementing-a-data-processing-extension.md)   
 [Reporting Services 延伸模組程式庫](../reporting-services-extension-library.md)  
  
  
