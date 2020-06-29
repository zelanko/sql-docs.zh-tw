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
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 690e73e0bda9cac2521cfec3fc6296c50fd3b69a
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/26/2020
ms.locfileid: "85436805"
---
# <a name="save-ssis-package-sql-server-import-and-export-wizard"></a>儲存 SSIS 封裝 (SQL Server 匯入和匯出精靈)
  使用 [**儲存 SSIS 封裝**] 頁面，即可命名、描述 Integration Services （）封裝，並將其儲存 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] 至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `msdb` 資料庫或副檔名為 .dtsx 的檔案。  
  
> [!NOTE]  
>  在 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 中，無法使用儲存此精靈所建立之封裝的選項。  
  
 若要深入瞭解此嚮導，請參閱[SQL Server 匯入和匯出嚮導](import-and-export-data-with-the-sql-server-import-and-export-wizard.md)。 若要瞭解啟動精靈的選項，以及成功執行嚮導所需的許可權，請參閱[執行 SQL Server 匯入和匯出嚮導](start-the-sql-server-import-and-export-wizard.md)。  
  
 「SQL Server 匯入和匯出精靈」的用途在於將資料從來源複製到目的地。 這個精靈也可以為您建立目的地資料庫和目的地資料表。 不過，如果您必須複製多個資料庫或資料表，或複製其他種類的資料庫物件，則應該改用「複製資料庫精靈」。 如需詳細資訊，請參閱 [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md)。  
  
## <a name="static-options"></a>靜態選項  
 **名稱**  
 提供封裝的唯一名稱。  
  
 **說明**  
 提供封裝的描述。 最佳作法是以其用途描述封裝，使封裝可以自我記錄並易於維護。  
  
 **目標**  
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
 當您選取檔案目的地時，請輸入目的地檔案的路徑，或使用 [**流覽]** 按鈕。  
  
 **瀏覽**  
 當您選取檔案目的地時，請使用 [**儲存封裝**] 對話方塊來流覽至目的地檔案。  
  
## <a name="see-also"></a>另請參閱  
 [儲存封裝](../save-packages.md)  
  
  
