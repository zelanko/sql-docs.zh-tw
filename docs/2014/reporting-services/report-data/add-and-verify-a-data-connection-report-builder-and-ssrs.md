---
title: 加入及驗證資料連接或資料來源 （報表產生器及 SSRS） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 1d3b2573-e29d-480d-9dde-d26379c86618
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 51ac8bee672064e07d66d924bc8efef0fc8aa1d5
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/22/2019
ms.locfileid: "59946434"
---
# <a name="add-and-verify-a-data-connection-or-data-source-report-builder-and-ssrs"></a>加入及驗證資料連接或資料來源 (報表產生器及 SSRS)
  在報表產生器中，您可以從報表伺服器加入共用資料來源，或是為您的報表建立內嵌資料來源。 在報表設計師中，您可以建立共用資料來源或內嵌資料來源，並將它部署至報表伺服器。  
  
 若要將共用資料來源加入至報表中，請瀏覽至報表伺服器，並選取共用資料來源。 報表中的共用資料來源會指向報表伺服器上的共用資料來源定義。  
  
 若要建立內嵌資料來源，您必須具有外部資料來源的連接資訊，而且必須知道存取資料必須擁有哪些權限。 這項資訊通常是來自於資料來源的擁有者。 您可以測試此連接，以確認指定的認證是否足夠。  
  
 如需詳細資訊，請參閱[報表產生器中的資料連接、資料來源及連接字串](../data-connections-data-sources-and-connection-strings-in-report-builder.md)和[在報表產生器中指定認證](../specify-credentials-in-report-builder.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-create-a-reference-to-a-shared-data-source"></a>建立共用資料來源的參考  
  
1.  在 [報表資料] 窗格的工具列上，按一下 **[新增]** ，然後按一下 **[資料來源]**。 **[資料來源屬性]** 對話方塊隨即開啟。  
  
2.  在 **[名稱]** 文字方塊中，輸入資料來源的名稱。  
  
    > [!NOTE]  
    >  這個名稱會儲存在本機報表定義中。 這個名稱不是共用資料來源在報表伺服器上的名稱。  
  
3.  選取 **[使用共用連接或報表模型]**。 隨即出現最近使用的共用資料來源和報表模型清單。 若要從報表伺服器選取其中一個項目，請按一下 **[瀏覽]** 並瀏覽至報表伺服器上提供共用資料來源的資料夾。  
  
4.  選取該共用資料來源，然後按一下 **[開啟]**。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 資料來源會出現在 [報表資料] 窗格中。  
  
### <a name="to-create-an-embedded-data-source"></a>建立內嵌資料來源  
  
1.  在 [報表資料] 窗格的工具列上，按一下 **[新增]**，然後按一下 **[資料來源]**。 **[資料來源屬性]** 對話方塊隨即開啟。  
  
2.  在 **[名稱]** 文字方塊中，輸入資料來源的名稱或接受預設值。  
  
3.  確認已選取 **[使用內嵌於我的報表的連接]** 。  
  
    1.  從 [選取連線類型] 下拉式清單中，選取資料來源類型，例如 [Microsoft SQL Server] 或 [OLE DB]。  
  
    2.  使用以下其中一個替代方式來指定連接字串：  
  
    -   在 **[連接字串]** 文字方塊中直接輸入連接字串。 如需連接字串範例的清單，請參閱 [報表產生器中的資料連接、資料來源及連接字串](../data-connections-data-sources-and-connection-strings-in-report-builder.md)。  
  
    -   按一下運算式 (**fx)** 按鈕，即可建立一個評估為連接字串的運算式。 在 **[運算式]** 對話方塊的 [運算式] 窗格內，輸入運算式。 [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
    -   按一下 **[建立]** ，針對您在步驟 2 中選擇的資料來源類型開啟 **[連接屬性]** 對話方塊。  
  
         依照此資料來源類型適合的情況，填入 **[連接屬性]** 對話方塊中的欄位。 連接屬性包括資料來源的類型、資料來源的名稱以及要使用的認證。 當您在此對話方塊中指定值之後，請按一下 **[測試連接]** 來確認此資料來源確實可用，而且您指定的認證正確無誤。  
  
4.  按一下 **[認證]**。  
  
     指定用於這個資料來源的認證。 資料來源的擁有者會選擇支援的認證類型。 在某些情況下，資料來源的擁有者會在報表伺服器上維護共用資料來源，並且使用您可以使用的認證來設定資料來源。 如需這項資訊，請連絡資料來源擁有者。 如需詳細資訊，請參閱 [在報表產生器中指定認證](../specify-credentials-in-report-builder.md)。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 資料來源會出現在 [報表資料] 窗格中。  
  
### <a name="to-verify-a-data-connection"></a>若要驗證資料連接  
  
1.  在工具列的 [報表資料] 窗格中，按兩下此資料來源。 **[資料來源屬性]** 對話方塊隨即開啟。  
  
2.  按一下 **[測試連接]**。  
  
3.  如果連線成功，便會出現下列訊息：「 已成功建立連線。 」 [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
4.  如果連線不成功，便會出現下列訊息：「 無法連接到資料來源。 」  
  
5.  按一下 **[詳細資料]**，並使用該資訊來更正問題。  
  
     如需詳細資訊，請參閱 [在報表產生器中指定認證](../specify-credentials-in-report-builder.md)。  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [將資料加入至報表&#40;報表產生器及 SSRS&#41;](report-datasets-ssrs.md)   
 [報表內嵌資料集和共用資料集 &#40;報表產生器及 SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [尋找、檢視和管理報表 &#40;報表產生器及 SSRS &#41;](../report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [報表產生器中的資料連接、資料來源及連接字串](../data-connections-data-sources-and-connection-strings-in-report-builder.md)  
  
  
