---
title: 指定預先部署或部署後指令碼
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
ms.assetid: 7f78f517-f13d-4f4b-84b9-e804cb490b2c
author: markingmyname
ms.author: maghan
manager: jroth
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: 56b69a6b84aa3c529c02690f7e6554e76e46b079
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "75244270"
---
# <a name="how-to-specify-predeployment-or-postdeployment-scripts"></a>如何：指定預先部署或部署後指令碼

預先部署和部署後指令碼會分別執行主要部署指令碼前後的 Transact\-SQL 陳述式，主要部署指令碼則是從資料庫專案產生。 從 Visual Studio 中的結構描述比較結果更新目標時，將不會執行預先部署指令碼。 專案中只能有一個預先部署指令碼和一個部署後指令碼。 這些指令碼有許多用途。 例如：  
  
-   預先部署指令碼可以從將要變更的資料表複製資料到暫存資料表，之後再由部署後指令碼將資料重新格式化並套用到所變更的資料表。  
  
-   您可以透過部署後指令碼，插入必須存在於資料表中的參考資料。 插入資料之前，可先測試該資料表是否已經包含資料。 如果資料表不是空的，您就必須清除現有的資料，或是指定您想要一律先重新建立資料庫，然後再部署它。 您可以將下列陳述式加入至部署後指令碼：  
  
```  
IF (EXISTS(SELECT * FROM [dbo].[MyReferenceTable]))  
BEGIN  
    DELETE FROM [dbo].[MyReferenceTable]  
END  
```  

## <a name="to-add-and-modify-a-pre--or-post-deployment-script"></a>若要加入和修改預先部署或部署後指令碼  
  
1.  在 [方案總管]  中，展開資料庫專案以顯示 [指令碼] 資料夾。  
  
2.  以滑鼠右鍵按一下 [指令碼] 資料夾，並選取 [加入]。  
  
3.  從內容功能表選取 [指令碼]。  
  
4.  選取 [預先部署指令碼] 或 [部署後指令碼]。 選擇性地指定非預設名稱。 按一下 [加入] 完成此步驟。  
  
5.  按兩下 [指令碼] 資料夾中的檔案。  
  
    Transact\-SQL 編輯器隨即開啟，其中顯示該檔案的內容。  
  
您可以在指令碼中使用 SQLCMD 語法和變數，並在資料庫專案屬性中設定這些項目。 例如：  
  
-   您可以在預先部署或部署後指令碼中使用 SQLCMD 語法納入檔案的內容。 系統會依照您定義的順序納入並執行各檔案：`:r .\myfile.sql`  
  
-   您可以在部署後指令碼中使用 SQLCMD 語法參考變數。 SQLCMD 變數則是在專案屬性或發行設定檔中進行設定：  
  
    ```  
    :setvar TableName MyTable  
    SELECT * FROM [$(TableName)]  
    ```  
  
如需在指令碼中使用 SQLCMD 的詳細資訊，請參閱[資料庫專案設定](../ssdt/database-project-settings.md)。  
  
## <a name="see-also"></a>另請參閱  
[專案導向的離線資料庫開發](../ssdt/project-oriented-offline-database-development.md)  
  
