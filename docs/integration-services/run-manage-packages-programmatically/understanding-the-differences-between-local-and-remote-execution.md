---
title: 了解本機和遠端執行之間的差異 | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- Integration Services packages, running
- packages [Integration Services], running
- packages [Integration Services], troubleshooting
ms.assetid: 610ee7d9-4fea-4aba-9395-57add826923b
author: chugugrace
ms.author: chugu
ms.openlocfilehash: c30d054c5a0c0e9a51d1799e919ba235c6a928fa
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/22/2020
ms.locfileid: "86913274"
---
# <a name="understanding-the-differences-between-local-and-remote-execution"></a>了解本機和遠端執行之間的差異

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  封裝開發人員與系統管理員應了解 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝的執行位置有其限制。  
  
-   **封裝會在其啟動程式的相同電腦上執行**。 即使當程式載入的封裝是儲存在遠端的另一台伺服器上，封裝仍然會在本機電腦上執行。  
  
-   **您只能在已安裝 Integration Services 的電腦之開發環境外部執行封裝**。 在未安裝 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 的用戶端電腦上，無法在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 的外部執行封裝，除此之外，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 授權的條款也可能不允許您在其他電腦上安裝 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 是伺服器元件，不可轉散發至用戶端電腦。 如果要從用戶端電腦執行封裝，必須以封裝能夠在伺服器上執行的方式啟動。  
  
 如需有關載入和執行儲存之封裝的詳細資訊，請參閱：  
  
-   [以程式設計方式載入和執行本機套件](../../integration-services/run-manage-packages-programmatically/loading-and-running-a-local-package-programmatically.md)  
  
-   [以程式設計方式載入和執行遠端套件](../../integration-services/run-manage-packages-programmatically/loading-and-running-a-remote-package-programmatically.md)  
  
 如需有關執行封裝以及將其輸出載入自訂程式的詳細資訊，請參閱：  
  
-   [載入本機套件的輸出](../../integration-services/run-manage-packages-programmatically/loading-the-output-of-a-local-package.md)  
  
## <a name="see-also"></a>另請參閱  
 [以程式設計方式載入和執行本機封裝](../../integration-services/run-manage-packages-programmatically/loading-and-running-a-local-package-programmatically.md)   
 [以程式設計方式載入和執行遠端封裝](../../integration-services/run-manage-packages-programmatically/loading-and-running-a-remote-package-programmatically.md)   
 [載入本機套件的輸出](../../integration-services/run-manage-packages-programmatically/loading-the-output-of-a-local-package.md)  
  
  
