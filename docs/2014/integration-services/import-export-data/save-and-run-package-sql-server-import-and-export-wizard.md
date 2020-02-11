---
title: 儲存並執行封裝（SQL Server 匯入和匯出嚮導） |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.saveschedule.f1
ms.assetid: b582c462-3d7a-4a4c-a2a2-2c79fedab75a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 517ba30e4565ec05e5fa15a650bb39909d24dd02
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62894762"
---
# <a name="save-and-execute-package-sql-server-import-and-export-wizard"></a>儲存並執行封裝 (SQL Server 匯入和匯出精靈)
  使用 [**儲存並執行封裝**] 對話方塊，即可立即執行封裝、儲存以供稍後執行或兩者。  
  
> [!NOTE]  
>  如果您在執行完成之前停止封裝，則不會儲存封裝，即使您選取 [**儲存**] 核取方塊也一樣。  
  
 若要深入瞭解此嚮導，請參閱[SQL Server 匯入和匯出嚮導](import-and-export-data-with-the-sql-server-import-and-export-wizard.md)。 若要瞭解用來啟動精靈的選項，以及成功執行嚮導所需的許可權，請參閱[執行 SQL Server 匯入和匯出嚮導](start-the-sql-server-import-and-export-wizard.md)。  
  
 「SQL Server 匯入和匯出精靈」的用途在於將資料從來源複製到目的地。 這個精靈也可以為您建立目的地資料庫和目的地資料表。 不過，如果您必須複製多個資料庫或資料表，或複製其他種類的資料庫物件，則應該改用「複製資料庫精靈」。 如需詳細資訊，請參閱 [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md)。  
  
## <a name="options"></a>選項。  
 **立即執行**  
 選取此選項即可立即執行封裝。  
  
 **儲存 SSIS 封裝**  
 儲存封裝供稍後執行，具有立即執行的選項。  
  
> [!NOTE]  
>  在 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 中，無法使用儲存此精靈所建立之封裝的選項。  
  
 **SQL Server**  
 選取此選項可將封裝儲存至[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `msdb`資料庫。  
  
> [!NOTE]  
>  只有當您已選取 [**儲存 SSIS 封裝**] 選項時，才能使用此選項。  
  
 **檔案系統**  
 選取此選項即可將封裝儲存為具有 .dtsx 副檔名的檔案。  
  
> [!NOTE]  
>  只有當您已選取 [**儲存 SSIS 封裝**] 選項時，才能使用此選項。  
  
 **封裝保護層級**  
 從清單中選取保護等級。  
  
 保護等級會決定保護方法、密碼或使用者金鑰，以及封裝保護的範圍。 保護可包括所有資料或只包括機密資料。 若要瞭解封裝安全性的需求和選項，請參閱[封裝中的敏感性資料存取控制](../security/access-control-for-sensitive-data-in-packages.md)和[安全性總覽 &#40;Integration Services&#41;](../security/security-overview-integration-services.md)。  
  
> [!NOTE]  
>  只有當您已選取 [**儲存 SSIS 封裝**] 選項時，才能使用此選項。  
  
 **密碼**  
 輸入密碼。  
  
> [!NOTE]  
>  只有在您已將 [**封裝保護等級**] 選項設定為 [以**密碼加密機密資料**] 或 [**以密碼加密所有資料**] 時，才可以使用此選項。  
  
 **重新輸入密碼**  
 再輸入密碼一次。  
  
> [!NOTE]  
>  只有在您已將 [**封裝保護等級**] 選項設定為 [以**密碼加密機密資料**] 或 [**以密碼加密所有資料**] 時，才可以使用此選項。  
  
## <a name="see-also"></a>另請參閱  
 [執行專案和套件](../packages/run-integration-services-ssis-packages.md)   
 [儲存封裝](../save-packages.md)  
  
  
