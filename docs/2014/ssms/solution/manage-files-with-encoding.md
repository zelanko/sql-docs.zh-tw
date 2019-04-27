---
title: 利用編碼管理檔案 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- files [SQL Server Management Studio]
- encoding [SQL Server Management Studio]
- files [SQL Server Management Studio], encoding
ms.assetid: 919544c9-59f0-4cc6-bb2a-f1ad671eb74b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 22b1c18cba793d5845e2adf92b1dca300911a72f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62823795"
---
# <a name="manage-files-with-encoding"></a>利用編碼管理檔案
  為了有助於在特定語言和特定平台中顯示您的程式碼，您可以建立檔案與特定字元編碼的關聯。  
  
## <a name="opening-files"></a>開啟檔案  
 您可以選擇用來編輯檔案的編輯器。  
  
#### <a name="to-open-a-file-with-a-specific-editor"></a>利用特定編輯器開啟檔案  
  
1.  在 [檔案] 功能表上，指向 [開啟舊檔]，再按一下 [檔案]。  
  
2.  在 [開啟檔案] 對話方塊中，選取檔案名稱。  
  
3.  按一下 [開啟舊檔] 按鈕旁的箭頭，在出現的功能表上，按一下 [開啟檔案]。  
  
4.  在 [選取要開啟的程式] 清單中，選取一個編輯器，再按一下 [開啟]。 若要開啟含有特定編碼的檔案，請選取含編碼支援的編輯器，如含編碼的 SQL 查詢編輯器，或含編碼的 XML 編輯器。  
  
## <a name="saving-files"></a>儲存檔案  
 您也可以利用 Unicode 編碼或不同的字碼頁來儲存您的程式碼，以便支援不同的語言，如西歐或東歐。 您可以建立特定字元編碼與檔案的關聯，以便用這個語言來顯示您的程式碼，也可以建立行尾結束符號類型的關聯，以便支援特定作業系統。 另外，當您在檔案名稱中使用某些字元時，除非用 Unicode 編碼來儲存，否則無法儲存它們。  
  
#### <a name="to-save-a-file-with-a-different-encoding-or-line-ending-type"></a>利用不同編碼或行尾結束符號類型來儲存檔案  
  
1.  在上**檔案**功能表上，按一下**儲存\<檔名 > 為**。  
  
2.  在 [另存新檔] 對話方塊中，展開 [儲存] 按鈕，再按一下 [使用編碼方式儲存]。  
  
3.  在 [進階儲存選項] 對話方塊中，從 [編碼] 清單中選取您需要的編碼。  
  
4.  從 [行尾結束符號] 清單中，選取您需要的行尾結束符號類型。  
  
    > [!NOTE]  
    >  如果您利用 Unicode 編碼來儲存您的檔案，檔案應該做為二進位檔簽入 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual SourceSafe 中，因為 Visual SourceSafe 不支援合併、比較和顯示儲存成 Unicode 的檔案之間的差異。  
  
 如果您利用 Visual SourceSafe，以 ANSI、UTF8 或 Unicode 來儲存檔案，請注意下列限制：  
  
-   ANSI 檔案只接受限制國際使用的目前字碼頁所支援的字元。  
  
-   Unicode 檔案無法使用共用的簽出、差異檢查或合併功能，因為它們是做為二進位檔來處理。 您可以在國際檔案中使用這個格式。  
  
-   UTF8 檔案無法與 Visual SourceSafe 一起安全地運作，因為在簽入、簽出、差異檢查和合併期間會進行變更，這些變更會使 UTF8 檔案編輯器發生問題。  
  
## <a name="see-also"></a>另請參閱  
 [管理方案和專案的檔案](files-that-manage-solutions-and-projects.md)   
 [使副檔名與程式碼編輯器相關聯](../../relational-databases/scripting/associate-file-extensions-to-a-code-editor.md)  
  
  
