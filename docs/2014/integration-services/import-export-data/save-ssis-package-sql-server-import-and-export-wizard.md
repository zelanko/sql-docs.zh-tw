---
title: 儲存 SSIS 套件 (SQL Server 匯入和匯出精靈) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.savedtspackage.f1
ms.assetid: 7bf8ac6a-5599-43ab-bf5c-e072c11b85a0
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 6af26cafd4f8dd9bf874ae7860c4f796bef48ae1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62892749"
---
# <a name="save-ssis-package-sql-server-import-and-export-wizard"></a>儲存 SSIS 封裝 (SQL Server 匯入和匯出精靈)
  使用**儲存 SSIS 封裝**名稱、 描述，並儲存頁面[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Integration Services ([!INCLUDE[ssIS](../../includes/ssis-md.md)]) 來封裝[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]`msdb`資料庫或檔案具有.dtsx延伸模組。  
  
> [!NOTE]  
>  在 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 中，無法使用儲存此精靈所建立之封裝的選項。  
  
 若要深入了解此精靈，請參閱[SQL Server 匯入和匯出精靈](import-and-export-data-with-the-sql-server-import-and-export-wizard.md)。 若要深入了解啟動精靈，選項和相關的權限，才能成功執行精靈，請參閱[執行 SQL Server 匯入和匯出精靈](start-the-sql-server-import-and-export-wizard.md)。  
  
 「SQL Server 匯入和匯出精靈」的用途在於將資料從來源複製到目的地。 這個精靈也可以為您建立目的地資料庫和目的地資料表。 不過，如果您必須複製多個資料庫或資料表，或複製其他種類的資料庫物件，則應該改用「複製資料庫精靈」。 如需詳細資訊，請參閱 [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md)。  
  
## <a name="static-options"></a>靜態選項  
 **名稱**  
 提供封裝的唯一名稱。  
  
 **說明**  
 提供封裝的描述。 最佳作法是以其用途描述封裝，使封裝可以自我記錄並易於維護。  
  
 **Target**  
 檢視先前為目的地檔案指定的目標 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或檔案)。  
  
## <a name="target-dynamic-options"></a>目標動態選項  
  
### <a name="target--sql-server"></a>目標 = SQL Server  
 **伺服器名稱**  
 當您已經選取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目的地時，請輸入或選取目的地伺服器名稱。  
  
 **[使用 Windows 驗證]**  
 當您已經選取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目的地時，請指定是否使用 Windows 整合式驗證連接到伺服器。 這是慣用的驗證方法。  
  
 **[使用 SQL Server 驗證]**  
 當您已經選取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目的地時，請指定是否使用 SQL Server 驗證連接到伺服器。  
  
 **使用者名稱**  
 當您已經選取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目的地，並且指定 SQL Server 驗證時，請輸入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用者名稱。  
  
 **密碼**  
 當您已經選取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目的地，並且指定 SQL Server 驗證時，請輸入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 密碼。  
  
### <a name="target--file-system"></a>目標 = 檔案系統  
 **檔案名稱**  
 當您選取檔案目的地時，請輸入目的地檔案的路徑，或使用**瀏覽** 按鈕。  
  
 **瀏覽**  
 當您選取檔案目的地時，使用瀏覽至目的地檔案**儲存封裝** 對話方塊。  
  
## <a name="see-also"></a>另請參閱  
 [儲存套件](../save-packages.md)  
  
  
