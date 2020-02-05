---
title: 在 SQL Server Data Tools 中複製封裝 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- packages [Integration Services], copying
- copying packages
- regenerating package GUID
- updating package properties
ms.assetid: 03edc659-e76d-48c0-a749-5f1899b6b507
author: chugugrace
ms.author: chugu
ms.openlocfilehash: b374955ea4a07cd94de88202fe02ffbb572d0a1c
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "71293644"
---
# <a name="copy-a-package-in-sql-server-data-tools"></a>在 SQL Server Data Tools 中複製封裝

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  此主題描述如何透過複製現有的封裝來建立新的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 封裝，以及如何更新這個新封裝的 **Name** 和 **GUID** 屬性。  
  
### <a name="to-copy-a-package"></a>若要複製封裝  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，開啟包含要複製之封裝的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，按兩下封裝。  
  
3.  確認是否已在「方案總管」中選取要複製的封裝，或「SSIS 設計師」中包含封裝的索引標籤是否為使用中的索引標籤。  
  
4.  在 [檔案]  功能表上，按一下 [另存 **封裝名稱> 為]\<** 。  
  
    > [!NOTE]  
    >  您必須先在 SSIS 設計師中開啟封裝，[另存新檔]  選項才會出現在 [檔案]  功能表上。  
  
5.  (選擇性) 瀏覽到不同的資料夾。  
  
6.  更新封裝檔案的名稱。 請務必保留 .dtsx 的副檔名。  
  
7.  按一下 [檔案]  。  
  
8.  出現系統提示時，選擇是否更新封裝物件的名稱，以符合檔案名稱。 如果您按一下 **[是]** ，就會更新封裝的 **Name** 屬性。 新的封裝便會加入 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案，並在「 [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師」中開啟。  
  
9. (選擇性) 按一下 **[控制流程]** 索引標籤的背景，然後按一下 **[屬性]** 。  
  
10. 在 [屬性] 視窗中，按一下 ID 屬性的值，然後在下拉式清單中按一下 [**產生新的識別碼>]\<** 。  
  
11. 在 **[檔案]** 功能表上按一下 **[儲存選取項目]** 以儲存新封裝。  
  
## <a name="see-also"></a>另請參閱  
 [儲存封裝的複本](https://msdn.microsoft.com/library/21482a20-e420-4452-b7eb-8f9fa1929f31)   
 [在 SQL Server Data Tools 中建立封裝](../integration-services/create-packages-in-sql-server-data-tools.md)   
 [Integration Services &#40;SSIS&#41; 封裝](../integration-services/integration-services-ssis-packages.md)  
  
  
