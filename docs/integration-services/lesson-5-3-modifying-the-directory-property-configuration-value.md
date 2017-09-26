---
title: "步驟 3： 修改 Directory 屬性組態值 |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: ba2a091f-361c-4331-afe2-53b465164c36
caps.latest.revision: 29
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 881aab31aab8cc4dc339b5f399f8cd207feb6ebb
ms.contentlocale: zh-tw
ms.lasthandoff: 09/26/2017

---
# <a name="lesson-5-3---modifying-the-directory-property-configuration-value"></a>課程 5-3-修改 Directory 屬性組態值
在這項工作中，您會修改儲存在 SSISTutorial.dtsConfig 檔案中有關套件層級變數 `User::varFolderName`之 Value 屬性的組態設定。 這個變數會更新 Foreach 迴圈容器的 Directory 屬性。 修改過的值將指向您在上一項工作中建立的 **新範例資料** 資料夾。 在修改組態設定及執行套件之後，該變數將使用從組態檔擴展的值而不是原本設定在套件中的目錄值來更新 Directory 屬性。  
  
### <a name="to-modify-the-configuration-setting-of-the-directory-property"></a>若要修改 Directory 屬性的組態設定  
  
1.  在記事本或任何其他文字編輯器中，尋找及開啟您在上一項工作中使用封裝組態精靈所建立的 SSISTutorial.dtsConfig 組態檔。  
  
2.  變更 **[ConfiguredValue]** 元素的值，使它符合您在上一項工作中建立的 **新範例資料** 資料夾的路徑。 請勿用引號括住路徑。 如果 **New Sample Data** 資料夾位於磁碟機的根目錄層級 (例如 C:\\)，則更新的 XML 應該類似於下列範例：  
  
    `<?xml version="1.0"?><DTSConfiguration><DTSConfigurationHeading><DTSConfigurationFileInfo GeneratedBy="DOMAIN\UserName" GeneratedFromPackageName="Lesson 5" GeneratedFromPackageID="{F4475E73-59E3-478F-8EB2-B10AFA61D3FA}" GeneratedDate="6/10/2012 8:16:50 AM"/></DTSConfigurationHeading><Configuration ConfiguredType="Property" Path="\Package.Variables[User::varFolderName].Properties[Value]" ValueType="String"><ConfiguredValue></ConfiguredValue></Configuration></DTSConfiguration>`  
  
    當然，檔案中的標題資訊 **GeneratedBy**、 **GeneratedFromPackageID**和 **GeneratedDate** 將會有所不同。 要注意的元素是 **Configuration** 元素。 **變數的** Value `User::varFolderName`屬性現在會包含 C:\New Sample Data。  
  
3.  儲存變更，然後關閉文字編輯器。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
[步驟 4：測試第 5 課的教學課程封裝](../integration-services/lesson-5-4-testing-the-lesson-5-tutorial-package.md)  
  
  
  

