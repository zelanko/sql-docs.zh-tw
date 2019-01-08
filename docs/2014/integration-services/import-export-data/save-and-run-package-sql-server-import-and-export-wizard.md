---
title: 儲存並執行封裝 （SQL Server 匯入和匯出精靈） |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.saveschedule.f1
ms.assetid: b582c462-3d7a-4a4c-a2a2-2c79fedab75a
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: fc075a50f3b57cf4856dbcd2ee36c13b83d968d4
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52773370"
---
# <a name="save-and-execute-package-sql-server-import-and-export-wizard"></a>儲存並執行封裝 (SQL Server 匯入和匯出精靈)
  使用**儲存並執行套件**對話方塊，即可立即執行封裝，儲存供稍後執行，或兩者。  
  
> [!NOTE]  
>  如果您在執行完成停止之前，封裝不會儲存，即使您選取**儲存**核取方塊。  
  
 若要深入了解此精靈，請參閱[SQL Server 匯入和匯出精靈](import-and-export-data-with-the-sql-server-import-and-export-wizard.md)。 若要深入了解啟動精靈，以及成功執行精靈所需的權限的選項，請參閱[執行 SQL Server 匯入和匯出精靈](start-the-sql-server-import-and-export-wizard.md)。  
  
 「SQL Server 匯入和匯出精靈」的用途在於將資料從來源複製到目的地。 這個精靈也可以為您建立目的地資料庫和目的地資料表。 不過，如果您必須複製多個資料庫或資料表，或複製其他種類的資料庫物件，則應該改用「複製資料庫精靈」。 如需詳細資訊，請參閱 [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md)。  
  
## <a name="options"></a>選項。  
 **立即執行**  
 選取此選項即可立即執行封裝。  
  
 **儲存 SSIS 套件**  
 儲存封裝供稍後執行，具有立即執行的選項。  
  
> [!NOTE]  
>  在 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 中，無法使用儲存此精靈所建立之封裝的選項。  
  
 **SQL Server**  
 選取此選項可將封裝儲存到[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `msdb`資料庫。  
  
> [!NOTE]  
>  此選項才會提供您已選取**儲存 SSIS 封裝**選項。  
  
 **檔案系統**  
 選取此選項即可將封裝儲存為具有 .dtsx 副檔名的檔案。  
  
> [!NOTE]  
>  此選項才會提供您已選取**儲存 SSIS 封裝**選項。  
  
 **套件保護層級**  
 從清單中選取保護等級。  
  
 保護等級會決定保護方法、密碼或使用者金鑰，以及封裝保護的範圍。 保護可包括所有資料或只包括機密資料。 若要了解封裝安全性的選項與需求，請參閱[套件中敏感性資料的存取控制](../security/access-control-for-sensitive-data-in-packages.md)並[安全性概觀&#40;Integration Services&#41;](../security/security-overview-integration-services.md)。  
  
> [!NOTE]  
>  此選項才會提供您已選取**儲存 SSIS 封裝**選項。  
  
 **密碼**  
 輸入密碼。  
  
> [!NOTE]  
>  此選項才會提供您已設定**封裝保護層級**選項**機密資料以密碼加密**或是**所有資料以密碼都加密**。  
  
 **再次輸入密碼**  
 再輸入密碼一次。  
  
> [!NOTE]  
>  此選項才會提供您已設定**封裝保護層級**選項**機密資料以密碼加密**或是**所有資料以密碼都加密**。  
  
## <a name="see-also"></a>另請參閱  
 [執行專案和套件](../packages/run-integration-services-ssis-packages.md)   
 [儲存套件](../save-packages.md)  
  
  
