---
title: 步驟 3：修改 Directory 屬性組態值 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: ba2a091f-361c-4331-afe2-53b465164c36
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: cb83ac5bb1b811c23b782b01167c437e9b989518
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62767360"
---
# <a name="step-3-modifying-the-directory-property-configuration-value"></a>步驟 3：修改 Directory 屬性組態值
  在這項工作中，您會修改儲存在 SSISTutorial.dtsConfig 檔案中有關套件層級變數 `User::varFolderName`之 Value 屬性的組態設定。 這個變數會更新 Foreach 迴圈容器的 Directory 屬性。 修改過的值會指向`New Sample Data`您在上一個工作中建立的資料夾。 在修改組態設定及執行套件之後，該變數將使用從組態檔擴展的值而不是原本設定在套件中的目錄值來更新 Directory 屬性。  
  
### <a name="to-modify-the-configuration-setting-of-the-directory-property"></a>若要修改 Directory 屬性的組態設定  
  
1.  在記事本或任何其他文字編輯器中，尋找及開啟您在上一項工作中使用封裝組態精靈所建立的 SSISTutorial.dtsConfig 組態檔。  
  
2.  值變更**ConfiguredValue**項目比對的路徑`New Sample Data`您在上一個工作中建立的資料夾。 請勿用引號括住路徑。 如果`New Sample Data`資料夾位於您的磁碟機的根層級 (例如 c:\\)，則更新的 XML 應該類似以下的範例：  
  
     `<?xml version="1.0"?><DTSConfiguration><DTSConfigurationHeading><DTSConfigurationFileInfo GeneratedBy="DOMAIN\UserName" GeneratedFromPackageName="Lesson 5" GeneratedFromPackageID="{F4475E73-59E3-478F-8EB2-B10AFA61D3FA}" GeneratedDate="6/10/2012 8:16:50 AM"/></DTSConfigurationHeading><Configuration ConfiguredType="Property" Path="\Package.Variables[User::varFolderName].Properties[Value]" ValueType="String"><ConfiguredValue></ConfiguredValue></Configuration></DTSConfiguration>`  
  
     標題資訊`GeneratedBy`， `GeneratedFromPackageID`，並**GeneratedDate**將位於不同檔案，當然。 要注意的元素是 `Configuration` 元素。 `Value` 變數的 `User::varFolderName` 屬性現在將會包含 C:\New Sample Data。  
  
3.  儲存變更，然後關閉文字編輯器。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [步驟 4：測試第 5 課的教學課程封裝](../integration-services/lesson-5-4-testing-the-lesson-5-tutorial-package.md)  
  
  
