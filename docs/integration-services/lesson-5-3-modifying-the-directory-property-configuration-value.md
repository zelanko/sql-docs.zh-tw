---
title: 步驟 3：修改 Directory 屬性設定值 | Microsoft Docs
ms.custom: ''
ms.date: 01/08/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: ba2a091f-361c-4331-afe2-53b465164c36
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 09d4279501110d15eab2ca339e33ddb9ab0cee3f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65721212"
---
# <a name="lesson-5-3-modify-the-directory-property-configuration-value"></a>第 5-3 課：修改 Directory 屬性設定值

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



在此工作中，您會修改儲存在 **SSISTutorial.dtsConfig** 檔案中的組態設定，以便設定套件層級變數 `User::varFolderName` 的 **Value** 屬性。 該變數會更新 Foreach 迴圈容器的 **Directory** 屬性。 修改過的值會指向您在上一項工作中建立的 [New Sample Data]  資料夾。 在修改組態設定並執行套件之後，會更新組態檔中變數的 **Directory** 屬性。 之前，**Directory** 屬性值是套件的一部分。  
  
## <a name="modify-the-configuration-setting-of-the-directory-property"></a>修改 Directory 屬性的組態設定  
  
1.  在 [記事本] 或任何其他文字編輯器中，尋找並開啟您在上一項工作中使用 [套件設定精靈] 所建立的 **SSISTutorial.dtsConfig** 設定檔。  
  
2.  變更 **[ConfiguredValue]** 元素的值，使它符合您在上一項工作中建立的 **新範例資料** 資料夾的路徑。 請勿用引號括住路徑。 如果 [New Sample Data]  資料夾位於磁碟機的根目錄層級 (例如 **C:\\** )，則更新的 XML 應該類似於下列範例：  
  
    ```
    <?xml version="1.0"?>
    <DTSConfiguration>
      <DTSConfigurationHeading>
        <DTSConfigurationFileInfo GeneratedBy="DOMAIN\UserName" GeneratedFromPackageName="Lesson 5" GeneratedFromPackageID="{F4475E73-59E3-478F-8EB2-B10AFEE1D3FA}" GeneratedDate="6/10/2018 8:16:50 AM"/>
      </DTSConfigurationHeading>
      <Configuration ConfiguredType="Property" 
          Path="\Package.Variables[User::varFolderName].Properties[Value]" ValueType="String">
        <ConfiguredValue>C:\New Sample Data</ConfiguredValue>
      </Configuration>
    </DTSConfiguration>  
    ```

    您檔案中的標題資訊 **GeneratedBy**、**GeneratedFromPackageID** 和 **GeneratedDate** 會有所不同。 要注意的元素是 **Configuration** 元素。 `User::varFolderName` 變數的 **Value** 屬性現在會包含 **C:\New Sample Data**。  
  
3.  儲存變更，然後關閉文字編輯器。  
  
## <a name="go-to-next-task"></a>移至下一個工作  
[步驟 4：測試第 5 課套件](../integration-services/lesson-5-4-testing-the-lesson-5-tutorial-package.md)  
  
  
  
