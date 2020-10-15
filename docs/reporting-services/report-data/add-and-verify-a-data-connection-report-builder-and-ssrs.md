---
title: 新增及驗證資料連線 (報表產生器) | Microsoft Docs
description: 了解如何使用報表產生器來新增及驗證資料連線，以驗證指定的認證是否足夠。
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
ms.reviewer: ''
ms.custom: ''
ms.date: 03/01/2017
ms.openlocfilehash: cfddbdca35d24589b3fa87976cbfb547f14a46ee
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/09/2020
ms.locfileid: "91891788"
---
# <a name="add-and-verify-a-data-connection-report-builder-and-ssrs"></a>加入及驗證資料連接 (報表產生器及 SSRS)

在報表產生器中，您可以從報表伺服器加入共用資料來源，或是為您的報表建立內嵌資料來源。 在報表設計師中，您可以建立共用資料來源或內嵌資料來源，並將它部署至報表伺服器。

若要將共用資料來源加入至報表中，請瀏覽至報表伺服器，並選取共用資料來源。 報表中的共用資料來源會指向報表伺服器上的共用資料來源定義。

若要建立內嵌資料來源，您必須具有外部資料來源的連接資訊，而且必須知道存取資料必須擁有哪些權限。 這項資訊通常是來自於資料來源的擁有者。 您可以測試此連接，以確認指定的認證是否足夠。

如需詳細資訊，請參閱[建立資料連接字串 - 報表產生器 & SSRS](data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)，以及[在報表產生器中指定認證](./specify-credential-and-connection-information-for-report-data-sources.md?view=sql-server-2017) (機器翻譯)

> [!NOTE]  
> [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]

## <a name="to-create-a-connection-to-a-shared-data-source-in-report-builder"></a>在報表產生器中建立共用資料來源的連接

1. 在 [報表資料] 窗格的工具列上，按一下 **[新增]** ，然後按一下 **[資料來源]** 。 **[資料來源屬性]** 對話方塊隨即開啟。

2. 在 **[名稱]** 文字方塊中，輸入資料來源的名稱。

    > [!NOTE]  
    >  這個名稱會儲存在本機報表定義中。 這個名稱不是共用資料來源在報表伺服器上的名稱。 

3. 選取 **[使用共用連接或報表模型]** 。 隨即出現最近使用的共用資料來源和報表模型清單。 若要從報表伺服器選取其中一個項目，請按一下 **[瀏覽]** 並瀏覽至報表伺服器上提供共用資料來源的資料夾。

4. 選取該共用資料來源，然後按一下 **[開啟]** 。

5. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

資料來源會出現在 [報表資料] 窗格中。

### <a name="to-verify-a-data-connection"></a>若要驗證資料連接  

1. 在工具列的 [報表資料] 窗格中，按兩下此資料來源。 **[資料來源屬性]** 對話方塊隨即開啟。

2. 按一下 **[測試連接]** 。

3. 如果連線成功，即會出現下列訊息：「成功建立連線」。 [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

4. 如果連線不成功，即會出現下列訊息：「無法連線到資料來源。」  

5. 按一下 **[詳細資料]** ，並使用該資訊來更正問題。

    如需詳細資訊，請參閱 [在報表產生器中指定認證](./specify-credential-and-connection-information-for-report-data-sources.md?view=sql-server-2017)。

6. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

## <a name="see-also"></a>另請參閱

- [報表資料集 &#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)   
- [報表內嵌資料集和共用資料集 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)
- [尋找、檢視和管理報表 &#40;報表產生器及 SSRS &#41;](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)
- [建立資料連接字串 - 報表產生器 & SSRS](data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)