---
title: 設定記錄時，使用已儲存的組態檔 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- containers [Integration Services], logs
- logs [Integration Services], containers
ms.assetid: e5fdbbcb-94ca-4912-aa7c-0d89cebbd308
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b2adc326ef2e0bb593b0532a51a9a677821ae0e2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66060594"
---
# <a name="configure-logging-by-using-a-saved-configuration-file"></a>使用已儲存的組態檔來設定記錄
  此程序描述如何透過載入先前儲存的記錄組態檔，為封裝中的新容器設定記錄。  
  
 依預設，封裝中的所有容器都使用與其父容器相同的記錄組態。 例如，「Foreach 迴圈」中的工作會使用與「Foreach 迴圈」相同的記錄組態。  
  
### <a name="to-configure-logging-for-a-container"></a>若要設定容器的記錄  
  
1.  在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 **[SSIS]** 功能表上，按一下 **[記錄]** 。  
  
3.  展開封裝樹狀檢視，並選取要設定的容器。  
  
4.  在 [提供者與記錄]  索引標籤上，選取要用於容器的記錄檔。  
  
    > [!NOTE]  
    >  您只可在封裝層級建立記錄檔。 如需詳細資訊，請參閱[在 SQL Server Data Tools 中啟用封裝記錄功能](../../2014/integration-services/enable-package-logging-in-sql-server-data-tools.md)。  
  
5.  按一下 [詳細資料]  索引標籤，然後按一下 [載入]  。  
  
6.  尋找要使用的記錄組態檔，然後按一下 [開啟]  。  
  
7.  (選擇性) 在 [事件]  資料行中選取核取方塊，以選取要記錄的另一個記錄項目。 按一下 [進階]  ，選取此項目所要記錄的資訊類型。  
  
    > [!NOTE]  
    >  新容器可能會包含原來用於建立記錄組態之容器無法使用的其他記錄項目。 如果您要記錄這些其他記錄項目，則必須手動選取之。  
  
8.  若要儲存記錄組態的更新版本，請按一下 [儲存]  。  
  
9. 若要儲存已更新的封裝，請在 **[檔案]** 功能表上，按一下 **[儲存選取項目]** 。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services &#40;SSIS&#41; 記錄](performance/integration-services-ssis-logging.md)  
  
  
